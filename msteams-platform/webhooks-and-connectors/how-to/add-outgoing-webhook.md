---
title: Добавление пользовательских ботов в Microsoft Teams с исходяшими веб-оками
description: описывает, как добавить исходяющий веб-сайт
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams tabs outgoing webhook actionable message verify webhook
ms.openlocfilehash: 2fac6f42e27a4c8cb3d079ea281d458a4dfe41ed
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069178"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a><span data-ttu-id="8ac25-104">Добавление пользовательских ботов в Teams с исходяшими веб-оками</span><span class="sxs-lookup"><span data-stu-id="8ac25-104">Add custom bots to Teams with outgoing webhooks</span></span>

## <a name="outgoing-webhooks-in-teams"></a><span data-ttu-id="8ac25-105">Исходяние веб-сайтов в Teams</span><span class="sxs-lookup"><span data-stu-id="8ac25-105">Outgoing webhooks in Teams</span></span>

<span data-ttu-id="8ac25-106">Webhooks — это выдающийся способ интеграции Teams с внешними приложениями.</span><span class="sxs-lookup"><span data-stu-id="8ac25-106">Webhooks are an eminent way for Teams to integrate with external apps.</span></span> <span data-ttu-id="8ac25-107">Веб-ок — это, по сути, запрос POST, отправленный на URL-адрес вызова.</span><span class="sxs-lookup"><span data-stu-id="8ac25-107">A webhook is essentially a POST request sent to a callback URL.</span></span> <span data-ttu-id="8ac25-108">Исходяющие веб-оки позволяют пользователям отправлять сообщения на веб-службу без полного процесса создания ботов с [помощью Microsoft Bot Framework](https://dev.botframework.com/).</span><span class="sxs-lookup"><span data-stu-id="8ac25-108">Outgoing webhooks allow users to send messages to your web service without going through the full process of creating bots via the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span>

<span data-ttu-id="8ac25-109">Исходяющий веб-сайт отправляет данные Teams любой выбранной службе, способной принимать полезной нагрузки JSON.</span><span class="sxs-lookup"><span data-stu-id="8ac25-109">Outgoing webhook sends data from Teams to any chosen service capable of accepting a JSON payload.</span></span> <span data-ttu-id="8ac25-110">После добавления исходяющих веб-ок в команду он выступает в качестве бота и ищет сообщения в каналах с помощью **\@ упоминания**.</span><span class="sxs-lookup"><span data-stu-id="8ac25-110">After adding the outgoing webhooks to a team, it acts as a bot and looks for messages in channels using **\@mention**.</span></span> <span data-ttu-id="8ac25-111">Он отправляет уведомления внешним веб-службам и отвечает богатыми сообщениями, в том числе карточками и изображениями.</span><span class="sxs-lookup"><span data-stu-id="8ac25-111">It sends notifications to external web services and responds with rich messages, which include cards and images.</span></span>

## <a name="outgoing-webhook-key-features"></a><span data-ttu-id="8ac25-112">Исходяние ключевых функций веб-сайта</span><span class="sxs-lookup"><span data-stu-id="8ac25-112">Outgoing webhook key features</span></span>

| <span data-ttu-id="8ac25-113">Возможность</span><span class="sxs-lookup"><span data-stu-id="8ac25-113">Feature</span></span> | <span data-ttu-id="8ac25-114">Описание</span><span class="sxs-lookup"><span data-stu-id="8ac25-114">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="8ac25-115">Конфигурация scoped</span><span class="sxs-lookup"><span data-stu-id="8ac25-115">Scoped configuration</span></span>| <span data-ttu-id="8ac25-116">Webhooks имеют область действия на уровне группы.</span><span class="sxs-lookup"><span data-stu-id="8ac25-116">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="8ac25-117">Необходимо пройти процесс настройки для каждой команды, в которой необходимо добавить исходяющий веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="8ac25-117">You must go through the setup process for each team where you want to add your outgoing webhook.</span></span> |
| <span data-ttu-id="8ac25-118">Реактивное сообщение</span><span class="sxs-lookup"><span data-stu-id="8ac25-118">Reactive messaging</span></span>| <span data-ttu-id="8ac25-119">Пользователи должны использовать @mention для получения сообщений для веб-пользователя.</span><span class="sxs-lookup"><span data-stu-id="8ac25-119">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="8ac25-120">В настоящее время пользователи могут отправлять сообщения об исходяшем веб-сайте только в общедоступных каналах, а не в личной или частной области.</span><span class="sxs-lookup"><span data-stu-id="8ac25-120">Currently, users can only message an outgoing webhook in public channels and not within the personal or private scope.</span></span> |
|<span data-ttu-id="8ac25-121">Стандартный обмен сообщениями HTTP</span><span class="sxs-lookup"><span data-stu-id="8ac25-121">Standard HTTP message exchange</span></span>|<span data-ttu-id="8ac25-122">Ответы отображаются в той же цепочке, что и исходное сообщение запроса, и могут включать любое содержимое сообщений в рамках бота, например богатый текст, изображения, карты и эмодзи.</span><span class="sxs-lookup"><span data-stu-id="8ac25-122">Responses appear in the same chain as the original request message and can include any bot framework message content, for example, rich text, images, cards, and emojis.</span></span> <span data-ttu-id="8ac25-123">Несмотря на то, что исходяющие веб-пользователи могут использовать карты, они не могут использовать любые действия карт, за исключением `openURL` .</span><span class="sxs-lookup"><span data-stu-id="8ac25-123">Although outgoing webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="8ac25-124">Teams Поддержка метода API</span><span class="sxs-lookup"><span data-stu-id="8ac25-124">Teams API method support</span></span>|<span data-ttu-id="8ac25-125">Исходяющий веб-сайт отправляет HTTP POST веб-службе и обрабатывает ответ обратно.</span><span class="sxs-lookup"><span data-stu-id="8ac25-125">Outgoing webhook sends an HTTP POST to a web service and process a response back.</span></span> <span data-ttu-id="8ac25-126">Они не могут получить доступ к другим API, таким как извлечение списка или списка каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="8ac25-126">They cannot access any other APIs like retrieve the roster or list of channels in a team.</span></span>|

## <a name="creating-actionable-messages"></a><span data-ttu-id="8ac25-127">Создание сообщений с действиями</span><span class="sxs-lookup"><span data-stu-id="8ac25-127">Creating actionable messages</span></span>

<span data-ttu-id="8ac25-128">Карты соединители включают три видимые кнопки на карте.</span><span class="sxs-lookup"><span data-stu-id="8ac25-128">The connector cards include three visible buttons on the card.</span></span> <span data-ttu-id="8ac25-129">Каждая кнопка определяется в `potentialAction` свойстве сообщения с помощью `ActionCard` действий.</span><span class="sxs-lookup"><span data-stu-id="8ac25-129">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions.</span></span> <span data-ttu-id="8ac25-130">Каждый из них содержит тип ввода, текстовое поле, выбор даты `ActionCard` или список с несколькими вариантами выбора.</span><span class="sxs-lookup"><span data-stu-id="8ac25-130">Each `ActionCard` contains an input type; a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="8ac25-131">Каждое `ActionCard` действие имеет связанное действие, `HttpPOST` например.</span><span class="sxs-lookup"><span data-stu-id="8ac25-131">Each `ActionCard` action has an associated action, for example, `HttpPOST`.</span></span>

<span data-ttu-id="8ac25-132">Карточки соединителей поддерживают действия трех типов:</span><span class="sxs-lookup"><span data-stu-id="8ac25-132">Connector cards support three types of actions:</span></span>

| <span data-ttu-id="8ac25-133">Действие</span><span class="sxs-lookup"><span data-stu-id="8ac25-133">Action</span></span> | <span data-ttu-id="8ac25-134">Описание</span><span class="sxs-lookup"><span data-stu-id="8ac25-134">Description</span></span> |
| ------- | ----------- |
| `ActionCard` |<span data-ttu-id="8ac25-135">Представляет один или несколько типов ввода и связанные действия.</span><span class="sxs-lookup"><span data-stu-id="8ac25-135">Presents one or more input types and associated actions.</span></span>|
| `HttpPOST` | <span data-ttu-id="8ac25-136">Отправляет запрос POST на URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="8ac25-136">Sends a POST request to a URL.</span></span> |
| `OpenUri` |  <span data-ttu-id="8ac25-137">Открывает URI в отдельном браузере или приложении, необязательно нацелив различные URL-адреса на основе операционных систем.</span><span class="sxs-lookup"><span data-stu-id="8ac25-137">Opens a URI in a separate browser or app, optionally targets different URIs based on operating systems.</span></span>|

<span data-ttu-id="8ac25-138">Действие `ActionCard` поддерживает три типа входных данных:</span><span class="sxs-lookup"><span data-stu-id="8ac25-138">The `ActionCard` action supports three input types:</span></span>

| <span data-ttu-id="8ac25-139">Тип ввода</span><span class="sxs-lookup"><span data-stu-id="8ac25-139">Input type</span></span> | <span data-ttu-id="8ac25-140">Описание</span><span class="sxs-lookup"><span data-stu-id="8ac25-140">Description</span></span> |
| ------- | ----------- |
| `TextInput` | <span data-ttu-id="8ac25-141">Однострочная или многострочная текстовая область с необязательным ограничением длины.</span><span class="sxs-lookup"><span data-stu-id="8ac25-141">A single-line or multiline text field with an optional length limit.</span></span> |
| `DateInput` | <span data-ttu-id="8ac25-142">Селектор даты с необязательным селектором времени.</span><span class="sxs-lookup"><span data-stu-id="8ac25-142">A date selector with an optional time selector.</span></span> |
| `MultichoiceInput` | <span data-ttu-id="8ac25-143">Указанный список вариантов, предлагающий один выбор или несколько вариантов.</span><span class="sxs-lookup"><span data-stu-id="8ac25-143">A specified list of choices, offering either a single selection or multiple selections.</span></span>|

<span data-ttu-id="8ac25-144">`MultichoiceInput` поддерживает `style` свойство, которое управляет отображением полного расширенного списка.</span><span class="sxs-lookup"><span data-stu-id="8ac25-144">`MultichoiceInput` supports a `style` property that controls the display of a fully expanded list.</span></span> <span data-ttu-id="8ac25-145">Значение по умолчанию `style` зависит от `isMultiSelect` значения.</span><span class="sxs-lookup"><span data-stu-id="8ac25-145">The default value of `style` depends on the `isMultiSelect` value.</span></span>

| <span data-ttu-id="8ac25-146">`isMultiSelect` значение</span><span class="sxs-lookup"><span data-stu-id="8ac25-146">`isMultiSelect` value</span></span>  | <span data-ttu-id="8ac25-147">`style` Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8ac25-147">`style` default value</span></span>  |
| --- | --- |
| <span data-ttu-id="8ac25-148">`false` или не задано</span><span class="sxs-lookup"><span data-stu-id="8ac25-148">`false` or not specified</span></span> | <span data-ttu-id="8ac25-149">Стиль по умолчанию `compact`</span><span class="sxs-lookup"><span data-stu-id="8ac25-149">The default style is `compact`</span></span>|
| `true` | <span data-ttu-id="8ac25-150">Стиль по умолчанию `expanded`</span><span class="sxs-lookup"><span data-stu-id="8ac25-150">The default style is `expanded`</span></span> |

> [!NOTE]
> * <span data-ttu-id="8ac25-151">Введите как и , если вы хотите, чтобы список с несколькими `"isMultiSelect": true` `"style": true` выборами отображался в компактном стиле.</span><span class="sxs-lookup"><span data-stu-id="8ac25-151">Enter both `"isMultiSelect": true` and `"style": true`, if you want the multi-select list to be displayed in a compact style.</span></span>
> * <span data-ttu-id="8ac25-152">Выбор свойства в Teams то же самое, что и выбор свойства в `compact` `style` Microsoft `normal` `style` Outlook.</span><span class="sxs-lookup"><span data-stu-id="8ac25-152">Selecting `compact` for the `style` property in Teams is the same as selecting `normal` for the `style` property in Microsoft Outlook.</span></span>
> * <span data-ttu-id="8ac25-153">Веб-сайты поддерживают только Office 365 и адаптивные карточки.</span><span class="sxs-lookup"><span data-stu-id="8ac25-153">Webhooks support only Office 365 message back cards and adaptive cards.</span></span>

<span data-ttu-id="8ac25-154">Другие сведения о действиях карт соединители см. в справке **[Действия](/outlook/actionable-messages/card-reference#actions)** в справочной карточке сообщения.</span><span class="sxs-lookup"><span data-stu-id="8ac25-154">For all other details about connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="adding-outgoing-webhooks-to-your-app"></a><span data-ttu-id="8ac25-155">Добавление исходяющих веб-ок в приложение</span><span class="sxs-lookup"><span data-stu-id="8ac25-155">Adding outgoing webhooks to your app</span></span>

<span data-ttu-id="8ac25-156">**Сценарий.** Нажмите уведомления об изменении состояния на сервере Teams канала в приложение.</span><span class="sxs-lookup"><span data-stu-id="8ac25-156">**Scenario**: Push change status notifications on a Teams channel database server to your app.</span></span>  
<span data-ttu-id="8ac25-157">**Пример.** У вас есть бизнес-приложение, которое отслеживает все операции CRUD, сделанные для записей сотрудников Teams пользователей отдела кадров канала через Office 365 аренды.</span><span class="sxs-lookup"><span data-stu-id="8ac25-157">**Example**: You have a line-of-business app that tracks all CRUD operations made to employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a><span data-ttu-id="8ac25-158">1. Создайте URL-адрес на сервере приложения, чтобы принять и обработать запрос POST с полезной нагрузкой JSON</span><span class="sxs-lookup"><span data-stu-id="8ac25-158">1. Create a URL on your app's server to accept and process a POST request with a JSON payload</span></span>

<span data-ttu-id="8ac25-159">Ваша служба получает сообщения в стандартной схеме обмена сообщениями службы ботов Azure.</span><span class="sxs-lookup"><span data-stu-id="8ac25-159">Your service receives messages in a standard Azure bot service messaging schema.</span></span> <span data-ttu-id="8ac25-160">Соединитель платформы ботов — это служба RESTful, которая позволяет вашей службе обрабатывать обмен отформатированными сообщениями JSON с помощью протоколов HTTPS, как описано в [API службы Azure Bot.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)</span><span class="sxs-lookup"><span data-stu-id="8ac25-160">The bot framework connector is a RESTful service that empowers your service to process the interchange of JSON formatted messages via HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="8ac25-161">Кроме того, вы можете следовать [Microsoft Bot Framework SDK] для обработки и размыва сообщений.</span><span class="sxs-lookup"><span data-stu-id="8ac25-161">Alternatively, you can follow the [Microsoft Bot Framework SDK] to process and parse messages.</span></span> <span data-ttu-id="8ac25-162">См. также [о службе ботов Azure.](/azure/bot-service/bot-service-overview-introduction)</span><span class="sxs-lookup"><span data-stu-id="8ac25-162">See also [About Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span></span>


<span data-ttu-id="8ac25-163">Исходяющие веб-окки имеют область действия до уровня и видны `team` всем участникам группы.</span><span class="sxs-lookup"><span data-stu-id="8ac25-163">Outgoing webhooks are scoped to the `team` level and are visible to all the team members.</span></span> <span data-ttu-id="8ac25-164">Так же, как и **\@** бот, пользователям необходимо упомянуть имя исходятого веб-пользователя, чтобы вызвать его в канале.</span><span class="sxs-lookup"><span data-stu-id="8ac25-164">Just like a bot, users need to **\@mention** the name of the outgoing webhook to invoke it in the channel.</span></span>

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a><span data-ttu-id="8ac25-165">2. Создайте метод проверки исходятого маркера HMAC веб-ок</span><span class="sxs-lookup"><span data-stu-id="8ac25-165">2. Create a method to verify the outgoing webhook HMAC token</span></span>

#### <a name="hmac-signature-for-testing-with-code-example"></a><span data-ttu-id="8ac25-166">Подпись HMAC для тестирования с помощью примера кода</span><span class="sxs-lookup"><span data-stu-id="8ac25-166">HMAC signature for testing with code example</span></span>

<span data-ttu-id="8ac25-167">Использование примера входящие сообщения и id: "contoso" signingKeyDictionary {"contoso", "vqF0En+Z0ucuRTM/01o2GuhHH3hKKk/N2bOmlM31zaA=" }.</span><span class="sxs-lookup"><span data-stu-id="8ac25-167">Using example of inbound message and id: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="8ac25-168">Используйте значение "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" в авторизации загона запроса.</span><span class="sxs-lookup"><span data-stu-id="8ac25-168">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="8ac25-169">Чтобы убедиться, что служба получает вызовы только от Teams клиентов, Teams код HMAC в заговорке `hmac` HTTP.</span><span class="sxs-lookup"><span data-stu-id="8ac25-169">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` header.</span></span> <span data-ttu-id="8ac25-170">Всегда включал код в протокол проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8ac25-170">Always included the code in your authentication protocol.</span></span>

<span data-ttu-id="8ac25-171">Код всегда должен проверять подпись HMAC, включенную в запрос:</span><span class="sxs-lookup"><span data-stu-id="8ac25-171">Your code must always validate the HMAC signature included in the request:</span></span>

* <span data-ttu-id="8ac25-172">Создание маркера HMAC из тела запроса сообщения.</span><span class="sxs-lookup"><span data-stu-id="8ac25-172">Generate the HMAC token from the request body of the message.</span></span> <span data-ttu-id="8ac25-173">Для этого на большинстве платформ существуют стандартные библиотеки (см. в Node.js [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) или [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for \# C).</span><span class="sxs-lookup"><span data-stu-id="8ac25-173">There are standard libraries to do this on most platforms (see [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js or see [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="8ac25-174">Microsoft Teams использует стандартную криптографию HMAC SHA256.</span><span class="sxs-lookup"><span data-stu-id="8ac25-174">Microsoft Teams uses standard SHA256 HMAC cryptography.</span></span> <span data-ttu-id="8ac25-175">Необходимо преобразовать тело в массив byte в UTF8.</span><span class="sxs-lookup"><span data-stu-id="8ac25-175">You need to convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="8ac25-176">Вычисляйте хаш из массива byte  маркера безопасности, предоставляемого Teams при регистрации исходяшего веб-окка в Teams клиенте].</span><span class="sxs-lookup"><span data-stu-id="8ac25-176">Compute the hash from the byte array of the security token **provided by Teams** when you registered the outgoing webhook in the Teams client].</span></span> <span data-ttu-id="8ac25-177">См. [статью Создать исходяющий веб-сайт](#create-an-outgoing-webhook).</span><span class="sxs-lookup"><span data-stu-id="8ac25-177">See [Create an outgoing webhook](#create-an-outgoing-webhook).</span></span>
* <span data-ttu-id="8ac25-178">Преобразование hash в строку с помощью кодификации UTF-8.</span><span class="sxs-lookup"><span data-stu-id="8ac25-178">Convert the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="8ac25-179">Сравните строковую величину сгенерированного hash со значением, заданным в запросе HTTP.</span><span class="sxs-lookup"><span data-stu-id="8ac25-179">Compare the string value of the generated hash with the value provided in the HTTP request.</span></span>

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a><span data-ttu-id="8ac25-180">3. Создайте метод для отправки ответа на ошибку или успешность</span><span class="sxs-lookup"><span data-stu-id="8ac25-180">3. Create a method to send a success or failure response</span></span>

<span data-ttu-id="8ac25-181">Ответы из исходяющих веб-сайтов отображаются в той же цепочке ответов, что и исходное сообщение.</span><span class="sxs-lookup"><span data-stu-id="8ac25-181">Responses from your outgoing webhooks appear in the same reply chain as the original message.</span></span> <span data-ttu-id="8ac25-182">Когда пользователь выполняет запрос, Microsoft Teams выполняет синхронный http-запрос в службу, и код получает пять секунд для ответа на сообщение до времени и прекращения подключения.</span><span class="sxs-lookup"><span data-stu-id="8ac25-182">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="8ac25-183">Пример отклика</span><span class="sxs-lookup"><span data-stu-id="8ac25-183">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

> [!NOTE]
> * <span data-ttu-id="8ac25-184">Вы можете отправлять адаптивную карту, карточку героя и текстовые сообщения в виде вложений с исходяшим веб-сайтом.</span><span class="sxs-lookup"><span data-stu-id="8ac25-184">You can send Adaptive Card, Hero card, and text messages as attachment with outgoing webhook.</span></span>
> * <span data-ttu-id="8ac25-185">Форматирование поддержки карт.</span><span class="sxs-lookup"><span data-stu-id="8ac25-185">Cards support formatting.</span></span> <span data-ttu-id="8ac25-186">Дополнительные сведения см. в [виде карт формата с разметками.](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#formatting-cards-with-markdown)</span><span class="sxs-lookup"><span data-stu-id="8ac25-186">For more information, see [format cards with markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#formatting-cards-with-markdown).</span></span>

<span data-ttu-id="8ac25-187">Ниже приводится пример ответа адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="8ac25-187">Following codes are examples of an Adaptive Card response:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ac25-188">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ac25-188">C#/.NET</span></span>](#tab/dotnet)

```csharp
string content = await this.Request.Content.ReadAsStringAsync();
Activity incomingActivity = JsonConvert.DeserializeObject<Activity>(content);

var Card = new AdaptiveCard(new AdaptiveSchemaVersion("1.4"))
{
    Body = new List<AdaptiveElement>()
    {
        new AdaptiveTextBlock(){Text= $"Request sent by: {incomingActivity.From.Name}"},
        new AdaptiveImage(){Url=new Uri("https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6")},
        new AdaptiveTextBlock(){Text="Sample image for Adaptive Card.."}
    }
};

var attachment = new Attachment()
{
    ContentType = AdaptiveCard.ContentType,
    Content = Card
};

var sampleResponseActivity = new Activity
{
    Attachments = new [] { attachment }
};

return sampleResponseActivity;
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="8ac25-189">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ac25-189">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
var receivedMsg = JSON.parse(payload);
var responseMsg = JSON.stringify({
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "contentUrl": null,
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: " + receivedMsg.from.name
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card."
                    }
                ]
            },
            "name": null,
            "thumbnailUrl": null
        }
    ]
});
```

# <a name="json"></a>[<span data-ttu-id="8ac25-190">JSON</span><span class="sxs-lookup"><span data-stu-id="8ac25-190">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: Megan"
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card.."
                    }
                ]
            }
        }
    ]
}
```

* * *

## <a name="create-an-outgoing-webhook"></a><span data-ttu-id="8ac25-191">Создание исходящего веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="8ac25-191">Create an outgoing webhook</span></span>

1. <span data-ttu-id="8ac25-192">Выберите соответствующую команду и выберите **команду Manage** из (&#8226;&#8226;&#8226;) выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="8ac25-192">Select the appropriate team and choose **Manage team** from the (&#8226;&#8226;&#8226;) drop-down menu.</span></span>
1. <span data-ttu-id="8ac25-193">Выберите **вкладку Apps** из панели навигации.</span><span class="sxs-lookup"><span data-stu-id="8ac25-193">Choose the **Apps** tab from the navigation bar.</span></span>
1. <span data-ttu-id="8ac25-194">Из нижнего правого угла окна выберите **Создать исходяющий веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="8ac25-194">From the window's lower right corner select **Create an outgoing webhook**.</span></span>
1. <span data-ttu-id="8ac25-195">В результате всплывающее окно выполните необходимые поля:</span><span class="sxs-lookup"><span data-stu-id="8ac25-195">In the resulting popup window complete the required fields:</span></span>

>* <span data-ttu-id="8ac25-196">**Имя.** Название веб-страницы и @mention нажмите</span><span class="sxs-lookup"><span data-stu-id="8ac25-196">**Name**: The webhook title and @mention tap</span></span>
>* <span data-ttu-id="8ac25-197">**URL-адрес** вызова: конечная точка HTTPS, которая принимает полезной нагрузки JSON и получает запросы POST из Teams</span><span class="sxs-lookup"><span data-stu-id="8ac25-197">**Callback URL**: The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams</span></span>
>* <span data-ttu-id="8ac25-198">**Описание.** Подробные строки, которые отображаются в карточке профиля и панели мониторинга приложений на уровне команды.</span><span class="sxs-lookup"><span data-stu-id="8ac25-198">**Description**: A detailed string that appear in the profile card and the team-level App dashboard</span></span>
>* <span data-ttu-id="8ac25-199">**Изображение профиля:** необязательный значок приложения для вашего веб-пользователя</span><span class="sxs-lookup"><span data-stu-id="8ac25-199">**Profile Picture**: An optional app icon for your webhook</span></span>
>* <span data-ttu-id="8ac25-200">Выберите **кнопку Создать** из нижнего правого угла всплывающее окно, а исходяющий веб-сайт добавляется в каналы текущей группы.</span><span class="sxs-lookup"><span data-stu-id="8ac25-200">Select the **Create** button from the lower right corner of the pop-up window and the outgoing webhook are added to the current team's channels.</span></span>
>* <span data-ttu-id="8ac25-201">В следующем диалоговом окне отображается маркер безопасности кода проверки подлинности сообщений на основе хэширования [(HMAC),](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) который используется для проверки подлинности вызовов между Teams и назначенной внешней службой.</span><span class="sxs-lookup"><span data-stu-id="8ac25-201">The next dialog window displays an [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) security token that is used to authenticate calls between Teams and the designated outside service.</span></span>
>* <span data-ttu-id="8ac25-202">Исходяющий веб-сайт доступен пользователям группы, только если URL-адрес действителен, а маркеры проверки подлинности сервера и клиента равны, например, рукопожатие HMAC.</span><span class="sxs-lookup"><span data-stu-id="8ac25-202">The outgoing webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal for example, an HMAC handshake.</span></span>

## <a name="code-sample"></a><span data-ttu-id="8ac25-203">Пример кода</span><span class="sxs-lookup"><span data-stu-id="8ac25-203">Code sample</span></span>
|<span data-ttu-id="8ac25-204">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="8ac25-204">**Sample name**</span></span> | <span data-ttu-id="8ac25-205">**Описание**</span><span class="sxs-lookup"><span data-stu-id="8ac25-205">**Description**</span></span> | <span data-ttu-id="8ac25-206">**.NET**</span><span class="sxs-lookup"><span data-stu-id="8ac25-206">**.NET**</span></span> | <span data-ttu-id="8ac25-207">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="8ac25-207">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="8ac25-208">Исходящие веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="8ac25-208">Outgoing webhooks</span></span> | <span data-ttu-id="8ac25-209">Примеры создания **пользовательских ботов,** которые будут использоваться в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8ac25-209">Samples to create **Custom Bots** to be used in Microsoft Teams.</span></span>| [<span data-ttu-id="8ac25-210">View</span><span class="sxs-lookup"><span data-stu-id="8ac25-210">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [<span data-ttu-id="8ac25-211">View</span><span class="sxs-lookup"><span data-stu-id="8ac25-211">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

