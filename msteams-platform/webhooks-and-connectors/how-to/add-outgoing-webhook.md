---
title: Создание исходятого веб-окка
author: laujan
description: описывает, как создать исходяющий веб-сайт
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
keywords: teams tabs outgoing webhook actionable message verify webhook
ms.openlocfilehash: c02ff5388e47ba40056afcc1fcf5e8d7ad4437e8
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140339"
---
# <a name="create-outgoing-webhook"></a><span data-ttu-id="2a3f5-104">Создание исходятого веб-сайта</span><span class="sxs-lookup"><span data-stu-id="2a3f5-104">Create Outgoing Webhook</span></span>

<span data-ttu-id="2a3f5-105">Исходящем веб-ок действует как бот и поиск сообщений в каналах с помощью **@mention**.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-105">The Outgoing Webhook acts as a bot and search for messages in channels using **@mention**.</span></span> <span data-ttu-id="2a3f5-106">Он отправляет уведомления внешним веб-службам и отвечает богатыми сообщениями, в том числе карточками и изображениями.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-106">It sends notifications to external web services and responds with rich messages, which include cards and images.</span></span> <span data-ttu-id="2a3f5-107">Это помогает пропустить процесс создания ботов через [Microsoft Bot Framework](https://dev.botframework.com/).</span><span class="sxs-lookup"><span data-stu-id="2a3f5-107">It helps to skip the process of creating bots through the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span>

## <a name="key-features-of-outgoing-webhook"></a><span data-ttu-id="2a3f5-108">Ключевые функции исходя из webhook</span><span class="sxs-lookup"><span data-stu-id="2a3f5-108">Key features of Outgoing Webhook</span></span>

<span data-ttu-id="2a3f5-109">В следующей таблице представлены функции и описание исходяющих веб-ок:</span><span class="sxs-lookup"><span data-stu-id="2a3f5-109">The following table provides the features and description of Outgoing Webhooks:</span></span>

| <span data-ttu-id="2a3f5-110">Возможности</span><span class="sxs-lookup"><span data-stu-id="2a3f5-110">Features</span></span> | <span data-ttu-id="2a3f5-111">Description</span><span class="sxs-lookup"><span data-stu-id="2a3f5-111">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="2a3f5-112">Конфигурация scoped</span><span class="sxs-lookup"><span data-stu-id="2a3f5-112">Scoped configuration</span></span>| <span data-ttu-id="2a3f5-113">Webhooks имеют область действия на уровне группы.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-113">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="2a3f5-114">Обязательный процесс создания для каждого добавляет исходяющий веб-ок.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-114">Mandatory set up process for each adds an Outgoing Webhook.</span></span> |
| <span data-ttu-id="2a3f5-115">Реактивное сообщение</span><span class="sxs-lookup"><span data-stu-id="2a3f5-115">Reactive messaging</span></span>| <span data-ttu-id="2a3f5-116">Пользователи должны использовать @mention для получения сообщений для веб-пользователя.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-116">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="2a3f5-117">В настоящее время пользователи могут отправлять сообщения об исходяшем веб-окне только в общедоступных каналах, а не в личной или частной области.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-117">Currently, users can only message an Outgoing Webhook in public channels and not within the personal or private scope.</span></span> |
|<span data-ttu-id="2a3f5-118">Стандартный обмен сообщениями HTTP</span><span class="sxs-lookup"><span data-stu-id="2a3f5-118">Standard HTTP message exchange</span></span>|<span data-ttu-id="2a3f5-119">Ответы отображаются в той же цепочке, что и исходное сообщение запроса, и могут включать любое содержимое сообщения Bot Framework, например богатый текст, изображения, карты и эмодзи.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-119">Responses appear in the same chain as the original request message and can include any Bot Framework message content, for example, rich text, images, cards, and emojis.</span></span> <span data-ttu-id="2a3f5-120">Несмотря на то, что исходяющие веб-пользователи могут использовать карты, они не могут использовать любые действия, за исключением `openURL` .</span><span class="sxs-lookup"><span data-stu-id="2a3f5-120">Although Outgoing Webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="2a3f5-121">Teams Поддержка метода API</span><span class="sxs-lookup"><span data-stu-id="2a3f5-121">Teams API method support</span></span>|<span data-ttu-id="2a3f5-122">Исходяющие веб-окки отправляют СООБЩЕНИЕ HTTP в веб-службу и получают ответ.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-122">Outgoing Webhooks sends an HTTP POST to a web service and gets a response.</span></span> <span data-ttu-id="2a3f5-123">Они не могут получить доступ к другим API, например получить список или список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-123">They cannot access any other APIs, such as retrieve the roster or list of channels in a team.</span></span>|

## <a name="create-outgoing-webhooks"></a><span data-ttu-id="2a3f5-124">Создание исходяющих веб-ок</span><span class="sxs-lookup"><span data-stu-id="2a3f5-124">Create Outgoing Webhooks</span></span>

<span data-ttu-id="2a3f5-125">Создание исходяющих веб-ок и добавление пользовательских ботов в Teams.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-125">Create Outgoing Webhooks and add custom bots to Teams.</span></span>

<span data-ttu-id="2a3f5-126">**Создание исходятого веб-сайта**</span><span class="sxs-lookup"><span data-stu-id="2a3f5-126">**To create an Outgoing Webhook**</span></span>

1. <span data-ttu-id="2a3f5-127">Выберите **Teams** с левой области.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-127">Select **Teams** from the left pane.</span></span> <span data-ttu-id="2a3f5-128">На **Teams** отображается страница:</span><span class="sxs-lookup"><span data-stu-id="2a3f5-128">The **Teams** page appears:</span></span>

    ![Канал Teams ](~/assets/images/teamschannel.png)

1. <span data-ttu-id="2a3f5-130">На **Teams** выберите требуемую команду для создания исходятого веб-окка и выберите &#8226;&#8226;&#8226;.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-130">In the **Teams** page, select the required team to create an Outgoing Webhook and select the &#8226;&#8226;&#8226;.</span></span> <span data-ttu-id="2a3f5-131">В меню dropdown выберите **команду Manage:**</span><span class="sxs-lookup"><span data-stu-id="2a3f5-131">In the dropdown menu, select **Manage team**:</span></span>

    ![Создание исходятого веб-сайта](~/assets/images/outgoingwebhook1.png)

1. <span data-ttu-id="2a3f5-133">Выберите **вкладку Apps** на странице канала:</span><span class="sxs-lookup"><span data-stu-id="2a3f5-133">Select the **Apps** tab on the channel page:</span></span>

    ![Создание исходятого веб-окка](~/assets/images/outgoingwebhook2.png)

1. <span data-ttu-id="2a3f5-135">Выберите **Создать исходяющий веб-сайт:**</span><span class="sxs-lookup"><span data-stu-id="2a3f5-135">Select **Create an Outgoing Webhook**:</span></span>

    ![Создание исходяющих веб-ок](~/assets/images/outgoingwebhook3.png)

1. <span data-ttu-id="2a3f5-137">Введите следующие сведения на странице **Создание исходятого веб-сайта:**</span><span class="sxs-lookup"><span data-stu-id="2a3f5-137">Type the following details in the **Create an Outgoing Webhook** page:</span></span>

    * <span data-ttu-id="2a3f5-138">**Имя.** Название веб-страницы и вкладка @mention веб@mention.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-138">**Name**: The webhook title and @mention tab.</span></span>
    * <span data-ttu-id="2a3f5-139">**URL-адрес** вызова: конечная точка HTTPS, которая принимает полезной нагрузки JSON и получает запросы POST из Teams.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-139">**Callback URL**: The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams.</span></span>
    * <span data-ttu-id="2a3f5-140">**Описание.** Подробная строка, которая отображается в карточке профиля и панели мониторинга приложений на уровне команды.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-140">**Description**: A detailed string that appears in the profile card and the team-level App dashboard.</span></span>
    * <span data-ttu-id="2a3f5-141">**Изображение профиля:** значок приложения для веб-пользователя, который является необязательным.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-141">**Profile Picture**: An app icon for your webhook, which is optional.</span></span>

1. <span data-ttu-id="2a3f5-142">Нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-142">Select **Create**.</span></span> <span data-ttu-id="2a3f5-143">Исходяющий веб-сайт добавляется в канал текущей команды:</span><span class="sxs-lookup"><span data-stu-id="2a3f5-143">The Outgoing Webhook is added to the current team's channel:</span></span>

    ![создание исходятого веб-окка](~/assets/images/outgoingwebhook.png)

<span data-ttu-id="2a3f5-145">Появляется поле диалогов на основе хэш-кода проверки подлинности сообщений [(HMAC).](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)</span><span class="sxs-lookup"><span data-stu-id="2a3f5-145">A [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) dialogue box appears.</span></span> <span data-ttu-id="2a3f5-146">Это маркер безопасности, используемый для проверки подлинности вызовов между Teams и назначенной внешней службой.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-146">It is a security token used to authenticate calls between Teams and the designated outside service.</span></span>

>[!NOTE]
> <span data-ttu-id="2a3f5-147">Исходяющий веб-ок доступен пользователям команды, только если URL-адрес действителен, а маркеры проверки подлинности сервера и клиента равны.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-147">The Outgoing Webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal.</span></span> <span data-ttu-id="2a3f5-148">Например, рукопожатие HMAC.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-148">For example, an HMAC handshake.</span></span>

<span data-ttu-id="2a3f5-149">Следующий сценарий содержит сведения о добавлении исходя из webhook:</span><span class="sxs-lookup"><span data-stu-id="2a3f5-149">The following scenario provides the details to add an Outgoing Webhook:</span></span>

* <span data-ttu-id="2a3f5-150">Сценарий. Нажмите уведомления об изменении состояния на сервере Teams канала в приложение.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-150">Scenario: Push change status notifications on a Teams channel database server to your app.</span></span>
* <span data-ttu-id="2a3f5-151">Пример. У вас есть строка бизнес-приложения, отслеживает все операции CRUD, такие как создание, чтение, обновление и удаление.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-151">Example: You have a line of business app that tracks all CRUD operations, such as create, read, update, and delete.</span></span> <span data-ttu-id="2a3f5-152">Эти операции для записей сотрудников Teams пользователей отдела кадров по всему Office 365 аренды.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-152">These operations are made to the employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

# <a name="url-json-payload"></a>[<span data-ttu-id="2a3f5-153">Полезной нагрузки URL-адреса JSON</span><span class="sxs-lookup"><span data-stu-id="2a3f5-153">URL JSON payload</span></span>](#tab/urljsonpayload)
<span data-ttu-id="2a3f5-154">**Создайте URL-адрес на сервере приложения, чтобы принять и обработать запрос POST с помощью полезной нагрузки JSON**</span><span class="sxs-lookup"><span data-stu-id="2a3f5-154">**Create a URL on your app's server to accept and process a POST request with a JSON payload**</span></span>

<span data-ttu-id="2a3f5-155">Ваша служба получает сообщения в стандартной схеме обмена сообщениями службы ботов Azure.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-155">Your service receives messages in a standard Azure bot service messaging schema.</span></span> <span data-ttu-id="2a3f5-156">Соединитель Bot Framework — это служба RESTful, которая позволяет обрабатывать обмен отформатированными сообщениями JSON с помощью протоколов HTTPS, как описано в [API службы Azure Bot.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)</span><span class="sxs-lookup"><span data-stu-id="2a3f5-156">The Bot Framework connector is a RESTful service that empowers to process the interchange of JSON formatted messages through HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="2a3f5-157">Кроме того, вы можете следовать Microsoft Bot Framework SDK для обработки и размыва сообщений.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-157">Alternatively, you can follow the Microsoft Bot Framework SDK to process and parse messages.</span></span> <span data-ttu-id="2a3f5-158">Дополнительные сведения см. [в обзоре Службы ботов Azure.](/azure/bot-service/bot-service-overview-introduction)</span><span class="sxs-lookup"><span data-stu-id="2a3f5-158">For more information, see [overview of Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span></span>

<span data-ttu-id="2a3f5-159">Исходяющие веб-окки имеют область действия до уровня и видны `team` всем участникам группы.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-159">Outgoing Webhooks are scoped to the `team` level and are visible to all the team members.</span></span> <span data-ttu-id="2a3f5-160">Чтобы вызвать **\@ его** в канале, пользователям необходимо упомянуть имя исходятого веб-пользователя.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-160">Users need to **\@mention** the name of the Outgoing Webhook to invoke it in the channel.</span></span>

# <a name="verify-hmac-token"></a>[<span data-ttu-id="2a3f5-161">Проверка маркера HMAC</span><span class="sxs-lookup"><span data-stu-id="2a3f5-161">Verify HMAC token</span></span>](#tab/verifyhmactoken)
<span data-ttu-id="2a3f5-162">**Создание метода проверки исходятого маркера HMAC Веб-окка**</span><span class="sxs-lookup"><span data-stu-id="2a3f5-162">**Create a method to verify the Outgoing Webhook HMAC token**</span></span>

<span data-ttu-id="2a3f5-163">Использование примера входящие сообщения и ID: "contoso" signingKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhHH3hKKk/N2bOmlM31zaA=" }.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-163">Using example of inbound message and ID: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="2a3f5-164">Используйте значение "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" в авторизации загона запроса.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-164">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="2a3f5-165">Чтобы убедиться, что служба получает вызовы только от Teams клиентов, Teams код HMAC в заговорке авторизации `hmac` HTTP.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-165">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` authorization header.</span></span> <span data-ttu-id="2a3f5-166">Всегда включите код в протокол проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-166">Always include the code in your authentication protocol.</span></span>

<span data-ttu-id="2a3f5-167">Код всегда должен проверять подпись HMAC, включенную в запрос, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2a3f5-167">Your code must always validate the HMAC signature included in the request as follows:</span></span>

* <span data-ttu-id="2a3f5-168">Создание маркера HMAC из тела запроса сообщения.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-168">Generate the HMAC token from the request body of the message.</span></span> <span data-ttu-id="2a3f5-169">Существуют стандартные библиотеки для этого на большинстве платформ, таких как [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) для Node.js и [Teams](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) веб-страницы для C \# ).</span><span class="sxs-lookup"><span data-stu-id="2a3f5-169">There are standard libraries to do this on most platform, such as [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js and [Teams webhook sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="2a3f5-170">Microsoft Teams использует стандартную криптографию HMAC SHA256.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-170">Microsoft Teams uses standard SHA256 HMAC cryptography.</span></span> <span data-ttu-id="2a3f5-171">Необходимо преобразовать тело в массив byte в UTF8.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-171">You must convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="2a3f5-172">Вычисляйте хаш из массива byte маркера безопасности, предоставляемого Teams при регистрации исходяшего веб-сайта в Teams клиенте.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-172">Compute the hash from the byte array of the security token provided by Teams when you registered the Outgoing Webhook in the Teams client.</span></span> <span data-ttu-id="2a3f5-173">См. [статью Создание исходятого веб-окка](#create-outgoing-webhook).</span><span class="sxs-lookup"><span data-stu-id="2a3f5-173">See [create an Outgoing Webhook](#create-outgoing-webhook).</span></span>
* <span data-ttu-id="2a3f5-174">Преобразование hash в строку с помощью кодификации UTF-8.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-174">Convert the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="2a3f5-175">Сравните строковую величину сгенерированного hash со значением, заданным в запросе HTTP.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-175">Compare the string value of the generated hash with the value provided in the HTTP request.</span></span>

# <a name="method-to-respond"></a>[<span data-ttu-id="2a3f5-176">Способ ответа</span><span class="sxs-lookup"><span data-stu-id="2a3f5-176">Method to respond</span></span>](#tab/methodtorespond)
<span data-ttu-id="2a3f5-177">**Создание метода для отправки ответа на ошибку или успешность**</span><span class="sxs-lookup"><span data-stu-id="2a3f5-177">**Create a method to send a success or failure response**</span></span>

<span data-ttu-id="2a3f5-178">Ответы из исходяющих веб-сайтов отображаются в той же цепочке ответов, что и исходное сообщение.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-178">Responses from your Outgoing Webhooks appear in the same reply chain as the original message.</span></span> <span data-ttu-id="2a3f5-179">Когда пользователь выполняет запрос, Microsoft Teams выполняет синхронный http-запрос в службу, и код получает пять секунд для ответа на сообщение до времени и прекращения подключения.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-179">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="2a3f5-180">Пример отклика</span><span class="sxs-lookup"><span data-stu-id="2a3f5-180">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```
---

> [!NOTE]
> * <span data-ttu-id="2a3f5-181">Вы можете отправлять адаптивную карту, карточку героя и текстовые сообщения в виде вложений с исходяшим веб-сайтом.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-181">You can send Adaptive Card, Hero card, and text messages as attachment with Outgoing Webhook.</span></span>
> * <span data-ttu-id="2a3f5-182">Форматирование поддержки карт.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-182">Cards support formatting.</span></span> <span data-ttu-id="2a3f5-183">Дополнительные сведения см. в [виде карт формата с разметками.](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown)</span><span class="sxs-lookup"><span data-stu-id="2a3f5-183">For more information, see [format cards with markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).</span></span>

<span data-ttu-id="2a3f5-184">Ниже приводится пример ответа адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="2a3f5-184">Following codes are examples of an Adaptive Card response:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="2a3f5-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2a3f5-185">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="2a3f5-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="2a3f5-186">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="2a3f5-187">JSON</span><span class="sxs-lookup"><span data-stu-id="2a3f5-187">JSON</span></span>](#tab/json)

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

## <a name="code-sample"></a><span data-ttu-id="2a3f5-188">Пример кода</span><span class="sxs-lookup"><span data-stu-id="2a3f5-188">Code sample</span></span>

|<span data-ttu-id="2a3f5-189">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="2a3f5-189">**Sample name**</span></span> | <span data-ttu-id="2a3f5-190">**Description**</span><span class="sxs-lookup"><span data-stu-id="2a3f5-190">**Description**</span></span> | <span data-ttu-id="2a3f5-191">**.NET**</span><span class="sxs-lookup"><span data-stu-id="2a3f5-191">**.NET**</span></span> | <span data-ttu-id="2a3f5-192">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="2a3f5-192">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="2a3f5-193">Исходяние веб-ок</span><span class="sxs-lookup"><span data-stu-id="2a3f5-193">Outgoing Webhooks</span></span> | <span data-ttu-id="2a3f5-194">Образцы для создания пользовательских ботов, которые будут использоваться в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2a3f5-194">Samples to create custom bots to be used in Microsoft Teams.</span></span>| [<span data-ttu-id="2a3f5-195">View</span><span class="sxs-lookup"><span data-stu-id="2a3f5-195">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [<span data-ttu-id="2a3f5-196">View</span><span class="sxs-lookup"><span data-stu-id="2a3f5-196">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="see-also"></a><span data-ttu-id="2a3f5-197">См. также</span><span class="sxs-lookup"><span data-stu-id="2a3f5-197">See also</span></span>
* [<span data-ttu-id="2a3f5-198">Создание входящих веб-ок</span><span class="sxs-lookup"><span data-stu-id="2a3f5-198">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="2a3f5-199">Создание соединителя Office 365</span><span class="sxs-lookup"><span data-stu-id="2a3f5-199">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="2a3f5-200">Создание и отправка сообщений</span><span class="sxs-lookup"><span data-stu-id="2a3f5-200">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
