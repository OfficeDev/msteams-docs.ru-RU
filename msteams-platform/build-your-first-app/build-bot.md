---
title: Начать работу - Построить бота
author: girliemac
description: Быстро создайте Microsoft Teams бота, используя Microsoft Teams набор средств.
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: 2cbd90b293e8ac8343febc7b3d23278d5bb5bf82
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565888"
---
# <a name="create-your-first-bot-for-teams"></a><span data-ttu-id="acd1a-103">Создайте свой первый бот для Teams</span><span class="sxs-lookup"><span data-stu-id="acd1a-103">Create your first bot for Teams</span></span>

<span data-ttu-id="acd1a-104">Этот учебник научит вас строить базовое приложение бота.</span><span class="sxs-lookup"><span data-stu-id="acd1a-104">This tutorial teaches you to build a basic bot app.</span></span> <span data-ttu-id="acd1a-105">Бот выступает в качестве посредника между Teams пользователями и вашим веб-приложением или службой с разговорным интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="acd1a-105">A bot acts as an intermediary between Teams users and your web app or service with a conversational interface.</span></span> <span data-ttu-id="acd1a-106">Люди могут общаться с ботом, чтобы быстро получить информацию или инициировать рабочие процессы и задачи, выполняемые вашим сервисом.</span><span class="sxs-lookup"><span data-stu-id="acd1a-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="acd1a-107">Чему вы научитесь</span><span class="sxs-lookup"><span data-stu-id="acd1a-107">What you'll learn</span></span>

* <span data-ttu-id="acd1a-108">Создайте проект приложения и бота, используя Microsoft Teams набор средств для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="acd1a-108">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="acd1a-109">Поймите Teams приложений, отливных для ботов.</span><span class="sxs-lookup"><span data-stu-id="acd1a-109">Understand the Teams app configurations relevant to bots.</span></span>
* <span data-ttu-id="acd1a-110">Хост и запустить приложение локально с помощью локального решения туннелирования.</span><span class="sxs-lookup"><span data-stu-id="acd1a-110">Host and run an app locally using a localhost tunneling solution.</span></span>
* <span data-ttu-id="acd1a-111">Sideload и проверить бота в Teams.</span><span class="sxs-lookup"><span data-stu-id="acd1a-111">Sideload and test a bot in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acd1a-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="acd1a-112">Prerequisites</span></span>

<span data-ttu-id="acd1a-113">Убедитесь, что вы понимаете, как настроить и построить простой Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="acd1a-113">Ensure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="acd1a-114">Для получения дополнительной [информации, см Microsoft Teams.](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="acd1a-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span> 

## <a name="1-create-your-app-project"></a><span data-ttu-id="acd1a-115">1. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="acd1a-115">1. Create your app project</span></span>

<span data-ttu-id="acd1a-116">Приложение Microsoft Teams набор средств вам настроить следующие компоненты для приложения:</span><span class="sxs-lookup"><span data-stu-id="acd1a-116">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span> 

* <span data-ttu-id="acd1a-117">**Конфигурации приложений и леса, имеющие** отношение к ботам.</span><span class="sxs-lookup"><span data-stu-id="acd1a-117">**App configurations and scaffolding** relevant to bots.</span></span>
* <span data-ttu-id="acd1a-118">**Бот,** автоматически зарегистрированный в службе Microsoft Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="acd1a-118">**Bot** that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="acd1a-119">**Создание проекта приложения**</span><span class="sxs-lookup"><span data-stu-id="acd1a-119">**To create your app project**</span></span>

1. В Visual Studio Code выберите **Microsoft Teams левой** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: стороне активности и **выберите Создать новое Teams приложение.**

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Скриншот, показывающий, как создать приложение в Teams набор средств.":::

1. <span data-ttu-id="acd1a-122">По запросу вопишитесь на свой аккаунт Microsoft 365 разработки.</span><span class="sxs-lookup"><span data-stu-id="acd1a-122">When prompted, sign in with your Microsoft 365 development account.</span></span> 
1. <span data-ttu-id="acd1a-123">На экране проекта Select выберите ботов Conversation:</span><span class="sxs-lookup"><span data-stu-id="acd1a-123">On the Select project screen, select Conversation bots:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Скриншот, показывающий, как создать нового бота в Teams набор средств.":::

1. <span data-ttu-id="acd1a-125">На **экране проекта Configure** введите имя для бота.</span><span class="sxs-lookup"><span data-stu-id="acd1a-125">On the **Configure project** screen, enter a name for your bot.</span></span> <span data-ttu-id="acd1a-126">Это имя по умолчанию для вашего приложения, а также название каталога проекта приложения на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="acd1a-126">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="acd1a-127">Выберите **Создать новый Бот**  >  **Создать Бот Регистрация,** как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="acd1a-127">Select **Create a new Bot** > **Create Bot Registration** as shown in the following image:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Скриншот, показывающий именования нового бота в Teams набор средств.":::

    <span data-ttu-id="acd1a-129">В случае успеха, ваш новый бот будет иметь статус **Зарегистрированный.**</span><span class="sxs-lookup"><span data-stu-id="acd1a-129">If successful, your new bot will have a **Registered** status.</span></span> <span data-ttu-id="acd1a-130">Теперь ваш бот автоматически регистрируется в Microsoft Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="acd1a-130">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Скриншот с регистрацией нового бота в Teams набор средств.":::

1. <span data-ttu-id="acd1a-132">**Выберите** отделку в нижней части экрана и сохраните проект на вашей машине.</span><span class="sxs-lookup"><span data-stu-id="acd1a-132">Select **Finish** at the bottom of the screen and save your project on your machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="acd1a-133">2. Понимание компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="acd1a-133">2. Understand your app project components</span></span>

<span data-ttu-id="acd1a-134">Большая часть конфигураций приложений и строительных лесов настроены автоматически при создании проекта с помощью Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="acd1a-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="acd1a-135">Рассмотрим основные компоненты для создания бота:</span><span class="sxs-lookup"><span data-stu-id="acd1a-135">Let's look at the main components for building a bot:</span></span>

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Скриншот, показывающий эшафот проекта в Teams набор средств.":::

<span data-ttu-id="acd1a-137">Если вы создали вкладку в другом учебнике, приложение леса для бота отличается.</span><span class="sxs-lookup"><span data-stu-id="acd1a-137">If you created a tab in another tutorial, the app scaffolding for the bot is different.</span></span> <span data-ttu-id="acd1a-138">В отличие от вкладок, разработка ботов не требует создания каких-либо фронт-конечных веб-компонентов или использования Teams JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="acd1a-138">Unlike tabs, bot development doesn't require you to build any front-end web components or use the Teams JavaScript client SDK.</span></span>  <span data-ttu-id="acd1a-139">Вместо этого, леса использует [Microsoft Bot Framework](https://dev.botframework.com/), который является открытым исходным кодом SDK для создания интеллектуальных, корпоративного класса ботов, которые могут работать в Интернете, мобильный, и, конечно, Teams!</span><span class="sxs-lookup"><span data-stu-id="acd1a-139">Instead, the scaffolding uses the [Microsoft Bot Framework](https://dev.botframework.com/), which is an open-source SDK for building intelligent, enterprise-grade bots that can work on the web, mobile, and of course Teams!</span></span> 

<span data-ttu-id="acd1a-140">Файл, `botActivityHandler.js` расположенный в корневом каталоге проекта, является Teams обработчиком, который обрабатывает действия ботов, например, как бот реагирует на определенные сообщения.</span><span class="sxs-lookup"><span data-stu-id="acd1a-140">The `botActivityHandler.js` file, located in the root directory of your project, is the Teams-specific handler that handles bot activities, such as how the bot responds to specific messages.</span></span> <span data-ttu-id="acd1a-141">Леса приложения предоставляют `botActivityHandler.js` файл, расположенный в корневом каталоге вашего проекта, является Teams обработчиком, который обрабатывает действия бота, такие как, как бот реагирует на определенные сообщения.</span><span class="sxs-lookup"><span data-stu-id="acd1a-141">The app scaffolding provides a `botActivityHandler.js` file located in the root directory of your project, is the Teams specific handler that handles bot activities such as how the bot responds to specific messages.</span></span>

## <a name="3-securely-expose-your-localhost-to-the-internet"></a><span data-ttu-id="acd1a-142">3. Безопасно разоблачить ваш localhost в Интернете</span><span class="sxs-lookup"><span data-stu-id="acd1a-142">3. Securely expose your localhost to the internet</span></span>

<span data-ttu-id="acd1a-143">Взгляните на `index.js` файл, который создает сервер HTTP и обрабатывает маршрутизацию, чтобы прослушивать входящие запросы на вашего бота.</span><span class="sxs-lookup"><span data-stu-id="acd1a-143">Take a look at the `index.js` file, which creates an HTTP server and handles routing to listen for incoming requests to your bot.</span></span> <span data-ttu-id="acd1a-144">`/api/messages`URL-адрес конечной точки приложения для ответа на запросы клиентов:</span><span class="sxs-lookup"><span data-stu-id="acd1a-144">The `/api/messages` is your app's endpoint URL to respond to client requests:</span></span> 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

<span data-ttu-id="acd1a-145">Чтобы переставить запросы в логику бота, необходимо настроить общедоступный URL-адрес, `https://example.com/api/messages` например, вместо `https://localhost` .</span><span class="sxs-lookup"><span data-stu-id="acd1a-145">To forward the requests to your bot's logic, you must set up a publicly accessible URL, such as `https://example.com/api/messages`, instead of `https://localhost`.</span></span> <span data-ttu-id="acd1a-146">Поскольку ваше приложение работает от вашего локального хостинга в настоящее время, вы *должны туннель* сети.</span><span class="sxs-lookup"><span data-stu-id="acd1a-146">Because your app is running from your localhost currently, you must *tunnel* the network.</span></span>

<span data-ttu-id="acd1a-147">Туннелирование является протоколом, который позволяет транспортировать данные по сети.</span><span class="sxs-lookup"><span data-stu-id="acd1a-147">Tunneling is a protocol that allows you to transport data across a network.</span></span> <span data-ttu-id="acd1a-148">И localhost туннелирования дает вам связь между вашей местной машины и удаленного соединения.</span><span class="sxs-lookup"><span data-stu-id="acd1a-148">And localhost tunneling gives you a connection between your local machine and a remote connection.</span></span> <span data-ttu-id="acd1a-149">Чтобы безопасно выставить ваш localhost в Интернете, мы рекомендуем вам использовать инструмент третьей стороны называется, **ngrok**.</span><span class="sxs-lookup"><span data-stu-id="acd1a-149">To securely expose your localhost to the internet, we recommend you to use the 3rd party tool called, **ngrok**.</span></span> <span data-ttu-id="acd1a-150">Это даст вам безопасный URL.</span><span class="sxs-lookup"><span data-stu-id="acd1a-150">This will give you a secure URL.</span></span> 

1. <span data-ttu-id="acd1a-151">Перейти к [ngrok.com и](https://ngrok.com/download) следовать инструкциям по установке и настройке ngrok в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="acd1a-151">Go to the [ngrok.com](https://ngrok.com/download) site and follow the instruction to install and set up ngrok in your environment.</span></span> 
    
    <span data-ttu-id="acd1a-152">Добавьте полный путь к ngrok.exe, установленному в системе ПЕРЕМЕННАЯ среда PATH.</span><span class="sxs-lookup"><span data-stu-id="acd1a-152">Add the full path to the ngrok.exe file that you installed to the system PATH environment variable.</span></span> <span data-ttu-id="acd1a-153">Точные шаги специфичны для оболочки, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="acd1a-153">The exact steps are specific to the shell that you are using.</span></span>

1.  <span data-ttu-id="acd1a-154">После того как вы закончили настройку, откройте терминал и запустите `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="acd1a-154">After you have finished setting it up, open a terminal and run `ngrok http -host-header=rewrite 3978`.</span></span> 

    <span data-ttu-id="acd1a-155">Теперь ngrok предоставляет вам общедоступный, безопасный URL, который направляется вашему локальному хостингу в порту 3978, так что скопируйте URL HTTPS, например, как `https://287a4f4223bc.ngrok.io` показано на скриншоте ниже, так как Teams требует подключения HTTPS:</span><span class="sxs-lookup"><span data-stu-id="acd1a-155">Now ngrok provides you a public, secure URL that forwards to your localhost at port 3978, so copy the HTTPS URL, for example, `https://287a4f4223bc.ngrok.io` as shown in the screenshot below, since Teams requires HTTPS connections:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="Скриншот, показывающий туннелинг localhost с ngrok.":::

1. <span data-ttu-id="acd1a-157">Зарегистрируйте URL-адрес в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="acd1a-157">Register the URL in your app manifest.</span></span> 

## <a name="4-register-your-bot-endpoint"></a><span data-ttu-id="acd1a-158">4. Зарегистрируйте конечную точку бота</span><span class="sxs-lookup"><span data-stu-id="acd1a-158">4. Register your bot endpoint</span></span>

<span data-ttu-id="acd1a-159">Чтобы использовать бота в Teams, необходимо зарегистрировать его в службе Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="acd1a-159">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="acd1a-160">Это делается автоматически при настройке приложения с помощью Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="acd1a-160">This is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="acd1a-161">Вы все равно должны указать адрес конечной точки для получения и обработки сообщений пользователей или запросов, отправленных боту.</span><span class="sxs-lookup"><span data-stu-id="acd1a-161">You must still specify an endpoint address to receive and process user messages, or requests sent to the bot.</span></span> <span data-ttu-id="acd1a-162">Как правило, URL выглядит `https://HOST_URL/api/messages` как .</span><span class="sxs-lookup"><span data-stu-id="acd1a-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="acd1a-163">Вы можете настроить это в наборе инструментов.</span><span class="sxs-lookup"><span data-stu-id="acd1a-163">You can configure this in the toolkit.</span></span>

1. <span data-ttu-id="acd1a-164">В Visual Studio Code, **открытые Microsoft Teams набор средств**.</span><span class="sxs-lookup"><span data-stu-id="acd1a-164">In Visual Studio Code, open **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="acd1a-165">Выберите **Bots**  >  **Существующие регистрации ботов** и выберите бота, созданного во время настройки.</span><span class="sxs-lookup"><span data-stu-id="acd1a-165">Select **Bots** > **Existing bot registrations** and select the bot you created during setup.</span></span> 
1. <span data-ttu-id="acd1a-166">Например, **в поле адреса** бота введите URL ngrok, где вы раз размещения `https://287a4f4223bc.ngrok.io` бота и придаток `/api/messages` к нему:</span><span class="sxs-lookup"><span data-stu-id="acd1a-166">In the **Bot endpoint address** field, enter the ngrok URL, for example, `https://287a4f4223bc.ngrok.io`, where you're hosting the bot and append `/api/messages` to it:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="Скриншот, показывающий, как туннель localhost с ngrok.":::

    <span data-ttu-id="acd1a-168">Ваш бот сможет отвечать на сообщения в Teams, после правильной настройки конечной точки.</span><span class="sxs-lookup"><span data-stu-id="acd1a-168">Your bot will be able to respond to messages in Teams, after you set up the endpoint correctly.</span></span> 

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="acd1a-169">5. Создание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="acd1a-169">5. Build and run your app</span></span>

<span data-ttu-id="acd1a-170">Вы настроили URL-адрес для размещения бота и настроили его для обработки сообщений.</span><span class="sxs-lookup"><span data-stu-id="acd1a-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="acd1a-171">Пришло время, чтобы получить ваше приложение и работает.</span><span class="sxs-lookup"><span data-stu-id="acd1a-171">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="acd1a-172">В терминале перейдите в корневой каталог проекта приложения и `npm install` запустите.</span><span class="sxs-lookup"><span data-stu-id="acd1a-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="acd1a-173">Запуск `npm start` .</span><span class="sxs-lookup"><span data-stu-id="acd1a-173">Run `npm start`.</span></span>

   <span data-ttu-id="acd1a-174">В случае успеха, вы видите следующее сообщение, указывающее, что ваш бот слушает для деятельности на `localhost` вашем:</span><span class="sxs-lookup"><span data-stu-id="acd1a-174">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="acd1a-175">6. Sideload ваш бот в Teams</span><span class="sxs-lookup"><span data-stu-id="acd1a-175">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="acd1a-176">С вашим бот работает, вы можете установить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="acd1a-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="acd1a-177">Если вы еще не перегрузили приложение Teams и не затеяли проблемы, следуйте этим [инструкциям.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="acd1a-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="acd1a-178">В Visual Studio Code, выберите **F5** ключ для запуска Teams веб-клиента.</span><span class="sxs-lookup"><span data-stu-id="acd1a-178">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="acd1a-179">В диалоге установки приложения, **выберите Добавить для меня**.</span><span class="sxs-lookup"><span data-stu-id="acd1a-179">In the app install dialog, select **Add for me**.</span></span> 

   > [!Note]
   > <span data-ttu-id="acd1a-180">По умолчанию приложение добавляется к вашему сообщению 1:1 прямого чата, однако вы можете установить его в команду или чат, нажав на маленькую стрелку **рядом Добавить для меня**.</span><span class="sxs-lookup"><span data-stu-id="acd1a-180">By default, the app is added to your 1:1 direct chat message, however you can choose to install it to a team or chat by clicking the little arrow beside **Add for me**.</span></span> <span data-ttu-id="acd1a-181">В этом учебнике, давайте просто нажмите Добавить.</span><span class="sxs-lookup"><span data-stu-id="acd1a-181">In this tutorial, let’s just click Add.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="Скриншот, показывающий туннелинг localhost с ngrok.":::

## <a name="7-test-your-bot"></a><span data-ttu-id="acd1a-183">7. Проверьте своего бота</span><span class="sxs-lookup"><span data-stu-id="acd1a-183">7. Test your bot</span></span>

<span data-ttu-id="acd1a-184">Скажем " Привет" вашему боту.</span><span class="sxs-lookup"><span data-stu-id="acd1a-184">Let's say "Hello" to your bot.</span></span>

* <span data-ttu-id="acd1a-185">В поле для составления, отправить `Hello` сообщение.</span><span class="sxs-lookup"><span data-stu-id="acd1a-185">In the compose box, send a `Hello` message.</span></span>
    <span data-ttu-id="acd1a-186">Ваш бот отвечает чем-то вроде следующего сообщения:</span><span class="sxs-lookup"><span data-stu-id="acd1a-186">Your bot replies with something like the following message:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="Скриншот, показывающий, как пользователь говорит &quot;Привет&quot; Teams бота и получает ответ.":::

    <span data-ttu-id="acd1a-188">Теперь вы создали базовый Teams, который может общаться с пользователями один на один или в групповых настройках (каналы и чаты) 🎉.</span><span class="sxs-lookup"><span data-stu-id="acd1a-188">You have now created a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats) 🎉.</span></span>

## <a name="troubleshoot-your-bot"></a><span data-ttu-id="acd1a-189">Устранение неполадок вашего бота</span><span class="sxs-lookup"><span data-stu-id="acd1a-189">Troubleshoot your bot</span></span>

<span data-ttu-id="acd1a-190">Следующая информация может помочь, если у вас были проблемы с завершением этого учебника.</span><span class="sxs-lookup"><span data-stu-id="acd1a-190">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="acd1a-191">Бот не подключен к Teams</span><span class="sxs-lookup"><span data-stu-id="acd1a-191">Bot isn't connected to Teams</span></span>


<span data-ttu-id="acd1a-192">Если вы установили приложение, но бот не работает, убедитесь, что [бот подключен к каналу службы Azure Bot Teams *канал.*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="acd1a-192">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="acd1a-193">Важно понимать, что это не то же самое, что канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="acd1a-193">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="acd1a-194">В этом случае канал — это способ подключения службы Azure Bot к Teams или другому [поддерживаемому приложению microsoft или сторонних коммуникаций.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="acd1a-194">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="acd1a-195">См. также</span><span class="sxs-lookup"><span data-stu-id="acd1a-195">See also</span></span>

* [<span data-ttu-id="acd1a-196">Бот основы</span><span class="sxs-lookup"><span data-stu-id="acd1a-196">Bot basics</span></span>](../bots/bot-basics.md)
* [<span data-ttu-id="acd1a-197">Создайте личную вкладку для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="acd1a-197">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
* [<span data-ttu-id="acd1a-198">Посмотрите, Teams боты могут сделать с одним из наших образцов</span><span class="sxs-lookup"><span data-stu-id="acd1a-198">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="acd1a-199">Основы беседы для ботов</span><span class="sxs-lookup"><span data-stu-id="acd1a-199">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="acd1a-200">Рекомендации по дизайну</span><span class="sxs-lookup"><span data-stu-id="acd1a-200">Design guidelines</span></span>](../bots/design/bots.md) 
* [<span data-ttu-id="acd1a-201">Готовые к производству шаблоны пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="acd1a-201">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md)
* [<span data-ttu-id="acd1a-202">Бот аутентификации в Teams</span><span class="sxs-lookup"><span data-stu-id="acd1a-202">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="acd1a-203">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="acd1a-203">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="acd1a-204">Создайте бота без инструментария</span><span class="sxs-lookup"><span data-stu-id="acd1a-204">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a><span data-ttu-id="acd1a-205">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="acd1a-205">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="acd1a-206">Создание расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="acd1a-206">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
