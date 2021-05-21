---
title: Начало работы — сборка бота
author: girliemac
description: Быстро создайте Microsoft Teams с помощью Microsoft Teams набор средств.
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
# <a name="create-your-first-bot-for-teams"></a><span data-ttu-id="ce1b2-103">Создайте свой первый бот для Teams</span><span class="sxs-lookup"><span data-stu-id="ce1b2-103">Create your first bot for Teams</span></span>

<span data-ttu-id="ce1b2-104">В этом руководстве вы можете создать базовое бот-приложение.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-104">This tutorial teaches you to build a basic bot app.</span></span> <span data-ttu-id="ce1b2-105">Бот выступает в качестве посредника между Teams пользователями и вашим веб-приложением или службой с диалоговом интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-105">A bot acts as an intermediary between Teams users and your web app or service with a conversational interface.</span></span> <span data-ttu-id="ce1b2-106">Люди могут общаться с ботом, чтобы быстро получить информацию или инициировать рабочий процесс и задачи, выполняемые вашей службой.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="ce1b2-107">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="ce1b2-107">What you'll learn</span></span>

* <span data-ttu-id="ce1b2-108">Создайте проект приложения и бот с помощью Microsoft Teams набор средств для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-108">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="ce1b2-109">Понимание конфигураций Teams приложений, соответствующих ботам.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-109">Understand the Teams app configurations relevant to bots.</span></span>
* <span data-ttu-id="ce1b2-110">Хост и запуск приложения локально с помощью решения локальной туннельной туннели.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-110">Host and run an app locally using a localhost tunneling solution.</span></span>
* <span data-ttu-id="ce1b2-111">Боковой загрузки и тестирования бота в Teams.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-111">Sideload and test a bot in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce1b2-112">Предварительные условия</span><span class="sxs-lookup"><span data-stu-id="ce1b2-112">Prerequisites</span></span>

<span data-ttu-id="ce1b2-113">Убедитесь, что вы понимаете, как настроить и создать простое Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-113">Ensure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="ce1b2-114">Дополнительные сведения см. в [приложении Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="ce1b2-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span> 

## <a name="1-create-your-app-project"></a><span data-ttu-id="ce1b2-115">1. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="ce1b2-115">1. Create your app project</span></span>

<span data-ttu-id="ce1b2-116">В Microsoft Teams набор средств вы можете настроить следующие компоненты для приложения:</span><span class="sxs-lookup"><span data-stu-id="ce1b2-116">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span> 

* <span data-ttu-id="ce1b2-117">**Конфигурации приложений и леса, соответствующие** ботам.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-117">**App configurations and scaffolding** relevant to bots.</span></span>
* <span data-ttu-id="ce1b2-118">**Бот,** автоматически зарегистрированный в службе Microsoft Azure бота.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-118">**Bot** that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="ce1b2-119">**Создание проекта приложения**</span><span class="sxs-lookup"><span data-stu-id="ce1b2-119">**To create your app project**</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** в левой панели действий и выберите Создать новое :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **приложение Teams.**

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Снимок экрана, показывающий, как создать приложение в Teams набор средств.":::

1. <span data-ttu-id="ce1b2-122">При запросе впишитесь в Microsoft 365 учетную запись разработки.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-122">When prompted, sign in with your Microsoft 365 development account.</span></span> 
1. <span data-ttu-id="ce1b2-123">На экране Select project выберите боты conversation:</span><span class="sxs-lookup"><span data-stu-id="ce1b2-123">On the Select project screen, select Conversation bots:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Снимок экрана, показывающий создание нового бота в Teams набор средств.":::

1. <span data-ttu-id="ce1b2-125">На экране **Настройка проекта** введите имя бота.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-125">On the **Configure project** screen, enter a name for your bot.</span></span> <span data-ttu-id="ce1b2-126">Это имя по умолчанию для вашего приложения, а также имя каталога проектов приложений на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-126">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="ce1b2-127">Выберите **Создание нового bot** Create Bot  >  **Registration,** как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="ce1b2-127">Select **Create a new Bot** > **Create Bot Registration** as shown in the following image:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Снимок экрана, показывающий имя нового бота в Teams набор средств.":::

    <span data-ttu-id="ce1b2-129">В случае успешной работы новый бот будет иметь **зарегистрированный** статус.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-129">If successful, your new bot will have a **Registered** status.</span></span> <span data-ttu-id="ce1b2-130">Теперь бот автоматически регистрируется в службе Microsoft Azure бота.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-130">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Снимок экрана, показывающий регистрацию нового бота в Teams набор средств.":::

1. <span data-ttu-id="ce1b2-132">Выберите **Готово** в нижней части экрана и сохраните проект на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-132">Select **Finish** at the bottom of the screen and save your project on your machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="ce1b2-133">2. Понимание компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="ce1b2-133">2. Understand your app project components</span></span>

<span data-ttu-id="ce1b2-134">Большая часть конфигураций приложений и строительных лесов создается автоматически при создании проекта с помощью Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="ce1b2-135">Рассмотрим основные компоненты для создания бота:</span><span class="sxs-lookup"><span data-stu-id="ce1b2-135">Let's look at the main components for building a bot:</span></span>

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Снимок экрана, показывающий строительный леса проекта в Teams набор средств.":::

<span data-ttu-id="ce1b2-137">Если вы создали вкладку в другом учебнике, строительные леса приложений для бота отличаются.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-137">If you created a tab in another tutorial, the app scaffolding for the bot is different.</span></span> <span data-ttu-id="ce1b2-138">В отличие от вкладок, для разработки бота не требуется создавать какие-либо веб-компоненты переднего Teams клиента JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-138">Unlike tabs, bot development doesn't require you to build any front-end web components or use the Teams JavaScript client SDK.</span></span>  <span data-ttu-id="ce1b2-139">Вместо этого в строительных лесах используется [Microsoft Bot Framework](https://dev.botframework.com/)SDK с открытым исходным кодом для создания интеллектуальных корпоративных ботов, которые могут работать в Интернете, мобильных устройствах и, конечно, Teams!</span><span class="sxs-lookup"><span data-stu-id="ce1b2-139">Instead, the scaffolding uses the [Microsoft Bot Framework](https://dev.botframework.com/), which is an open-source SDK for building intelligent, enterprise-grade bots that can work on the web, mobile, and of course Teams!</span></span> 

<span data-ttu-id="ce1b2-140">Файл, расположенный в корневом каталоге проекта, является обработщиком Teams, который обрабатывает действия бота, например, как бот реагирует на определенные `botActivityHandler.js` сообщения.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-140">The `botActivityHandler.js` file, located in the root directory of your project, is the Teams-specific handler that handles bot activities, such as how the bot responds to specific messages.</span></span> <span data-ttu-id="ce1b2-141">Строительные леса приложений предоставляют файл, расположенный в корневом каталоге проекта, это специальный обработщик Teams который обрабатывает действия бота, например, как бот реагирует на определенные `botActivityHandler.js` сообщения.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-141">The app scaffolding provides a `botActivityHandler.js` file located in the root directory of your project, is the Teams specific handler that handles bot activities such as how the bot responds to specific messages.</span></span>

## <a name="3-securely-expose-your-localhost-to-the-internet"></a><span data-ttu-id="ce1b2-142">3. Надежно обналичите локальное подключение к Интернету</span><span class="sxs-lookup"><span data-stu-id="ce1b2-142">3. Securely expose your localhost to the internet</span></span>

<span data-ttu-id="ce1b2-143">Взгляните на файл, который создает http-сервер и обрабатывает маршрутику для прослушивания входящих `index.js` запросов к боту.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-143">Take a look at the `index.js` file, which creates an HTTP server and handles routing to listen for incoming requests to your bot.</span></span> <span data-ttu-id="ce1b2-144">Url-адрес конечной точки приложения `/api/messages` для ответа на запросы клиентов:</span><span class="sxs-lookup"><span data-stu-id="ce1b2-144">The `/api/messages` is your app's endpoint URL to respond to client requests:</span></span> 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

<span data-ttu-id="ce1b2-145">Чтобы переададировать запросы в логику бота, необходимо настроить общедоступный URL-адрес, например , вместо `https://example.com/api/messages` `https://localhost` .</span><span class="sxs-lookup"><span data-stu-id="ce1b2-145">To forward the requests to your bot's logic, you must set up a publicly accessible URL, such as `https://example.com/api/messages`, instead of `https://localhost`.</span></span> <span data-ttu-id="ce1b2-146">Так как в настоящее время приложение работает из локального приложения, необходимо *туннелить* сеть.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-146">Because your app is running from your localhost currently, you must *tunnel* the network.</span></span>

<span data-ttu-id="ce1b2-147">Tunneling — это протокол, который позволяет транспортировать данные по сети.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-147">Tunneling is a protocol that allows you to transport data across a network.</span></span> <span data-ttu-id="ce1b2-148">И локальное туннельное подключение обеспечивает подключение между локальной машиной и удаленным подключением.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-148">And localhost tunneling gives you a connection between your local machine and a remote connection.</span></span> <span data-ttu-id="ce1b2-149">Чтобы безопасно выставить локализованную сеть в Интернете, рекомендуется использовать средство 3-й стороны под названием **ngrok**.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-149">To securely expose your localhost to the internet, we recommend you to use the 3rd party tool called, **ngrok**.</span></span> <span data-ttu-id="ce1b2-150">Это даст вам безопасный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-150">This will give you a secure URL.</span></span> 

1. <span data-ttu-id="ce1b2-151">Перейдите на [ngrok.com](https://ngrok.com/download) и следуйте инструкции по установке и установке ngrok в среде.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-151">Go to the [ngrok.com](https://ngrok.com/download) site and follow the instruction to install and set up ngrok in your environment.</span></span> 
    
    <span data-ttu-id="ce1b2-152">Добавьте полный путь в файл ngrok.exe, установленный в переменную среды PATH системы.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-152">Add the full path to the ngrok.exe file that you installed to the system PATH environment variable.</span></span> <span data-ttu-id="ce1b2-153">Точные действия специфичная для оболочки, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-153">The exact steps are specific to the shell that you are using.</span></span>

1.  <span data-ttu-id="ce1b2-154">После завершения настройки откройте терминал и запустите `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="ce1b2-154">After you have finished setting it up, open a terminal and run `ngrok http -host-header=rewrite 3978`.</span></span> 

    <span data-ttu-id="ce1b2-155">Теперь ngrok предоставляет общедоступный защищенный URL-адрес, который передается в локальный адрес в порту 3978, поэтому скопируйте URL-адрес HTTPS, например, как показано на скриншоте ниже, так как для Teams требуется `https://287a4f4223bc.ngrok.io` подключение HTTPS:</span><span class="sxs-lookup"><span data-stu-id="ce1b2-155">Now ngrok provides you a public, secure URL that forwards to your localhost at port 3978, so copy the HTTPS URL, for example, `https://287a4f4223bc.ngrok.io` as shown in the screenshot below, since Teams requires HTTPS connections:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="Снимок экрана, показывающий туннельирование localhost с помощью ngrok.":::

1. <span data-ttu-id="ce1b2-157">Зарегистрируйте URL-адрес в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-157">Register the URL in your app manifest.</span></span> 

## <a name="4-register-your-bot-endpoint"></a><span data-ttu-id="ce1b2-158">4. Регистрация конечной точки бота</span><span class="sxs-lookup"><span data-stu-id="ce1b2-158">4. Register your bot endpoint</span></span>

<span data-ttu-id="ce1b2-159">Чтобы использовать бот в Teams, необходимо зарегистрировать его в службе Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-159">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="ce1b2-160">Это делается автоматически при настройках приложения с помощью Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-160">This is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="ce1b2-161">Для получения и обработки сообщений пользователей или запросов, отправленных боту, необходимо указать адрес конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-161">You must still specify an endpoint address to receive and process user messages, or requests sent to the bot.</span></span> <span data-ttu-id="ce1b2-162">Как правило, URL-адрес выглядит `https://HOST_URL/api/messages` как .</span><span class="sxs-lookup"><span data-stu-id="ce1b2-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="ce1b2-163">Это можно настроить в наборе инструментов.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-163">You can configure this in the toolkit.</span></span>

1. <span data-ttu-id="ce1b2-164">В Visual Studio Code откройте **Microsoft Teams набор средств**.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-164">In Visual Studio Code, open **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="ce1b2-165">Выберите **Боты**  >  **Существующие регистрации ботов** и выберите бот, созданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-165">Select **Bots** > **Existing bot registrations** and select the bot you created during setup.</span></span> 
1. <span data-ttu-id="ce1b2-166">В поле **адресов конечной точки** Бота введите URL-адрес ngrok, например, где размещен бот и `https://287a4f4223bc.ngrok.io` приложение к `/api/messages` ней:</span><span class="sxs-lookup"><span data-stu-id="ce1b2-166">In the **Bot endpoint address** field, enter the ngrok URL, for example, `https://287a4f4223bc.ngrok.io`, where you're hosting the bot and append `/api/messages` to it:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="Снимок экрана, показывающий, как туннель localhost с помощью ngrok.":::

    <span data-ttu-id="ce1b2-168">Ваш бот сможет отвечать на сообщения в Teams после правильного настройка конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-168">Your bot will be able to respond to messages in Teams, after you set up the endpoint correctly.</span></span> 

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="ce1b2-169">5. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="ce1b2-169">5. Build and run your app</span></span>

<span data-ttu-id="ce1b2-170">Вы настроили URL-адрес для хост-бота и настроили его для обработки сообщений.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="ce1b2-171">Пришло время, чтобы ваше приложение было запущено.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-171">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="ce1b2-172">В терминале перейдите в корневой каталог проекта приложения и запустите `npm install` .</span><span class="sxs-lookup"><span data-stu-id="ce1b2-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="ce1b2-173">Запуск `npm start` .</span><span class="sxs-lookup"><span data-stu-id="ce1b2-173">Run `npm start`.</span></span>

   <span data-ttu-id="ce1b2-174">В случае успеха вы увидите следующее сообщение, указывающее на то, что ваш бот прослушивает действия в `localhost` вашем :</span><span class="sxs-lookup"><span data-stu-id="ce1b2-174">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="ce1b2-175">6. Боковой загрузки бота в Teams</span><span class="sxs-lookup"><span data-stu-id="ce1b2-175">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="ce1b2-176">При запуске бота его можно установить в Teams.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="ce1b2-177">Если вы еще не перегружали приложение Teams и не могли работать с проблемой, следуйте [этим инструкциям.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="ce1b2-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="ce1b2-178">В Visual Studio Code выберите **клавишу F5** для запуска веб Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-178">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="ce1b2-179">В диалоговом окте установке приложения выберите **Добавить для меня**.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-179">In the app install dialog, select **Add for me**.</span></span> 

   > [!Note]
   > <span data-ttu-id="ce1b2-180">По умолчанию приложение добавляется в ваше прямое сообщение чата 1:1, однако вы можете установить его в команду или чат, щелкнув стрелку рядом **Добавить для меня**.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-180">By default, the app is added to your 1:1 direct chat message, however you can choose to install it to a team or chat by clicking the little arrow beside **Add for me**.</span></span> <span data-ttu-id="ce1b2-181">В этом руководстве давайте просто нажмите кнопку Добавить.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-181">In this tutorial, let’s just click Add.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="Снимок экрана, показывающий туннельный локальный канал с помощью ngrok.":::

## <a name="7-test-your-bot"></a><span data-ttu-id="ce1b2-183">7. Проверка бота</span><span class="sxs-lookup"><span data-stu-id="ce1b2-183">7. Test your bot</span></span>

<span data-ttu-id="ce1b2-184">Давайте скажем "Привет" вашему боту.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-184">Let's say "Hello" to your bot.</span></span>

* <span data-ttu-id="ce1b2-185">В окне составить отправьте `Hello` сообщение.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-185">In the compose box, send a `Hello` message.</span></span>
    <span data-ttu-id="ce1b2-186">Бот отвечает следующим сообщением:</span><span class="sxs-lookup"><span data-stu-id="ce1b2-186">Your bot replies with something like the following message:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="Снимок экрана, на котором пользователь скажет &quot;Привет&quot; Teams боту и получить ответ.":::

    <span data-ttu-id="ce1b2-188">Теперь вы создали базовый Teams, который может общаться с пользователями один на один или в групповых настройках (каналы и чаты) 🎉.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-188">You have now created a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats) 🎉.</span></span>

## <a name="troubleshoot-your-bot"></a><span data-ttu-id="ce1b2-189">Устранение неполадок в боте</span><span class="sxs-lookup"><span data-stu-id="ce1b2-189">Troubleshoot your bot</span></span>

<span data-ttu-id="ce1b2-190">Следующие сведения могут помочь, если у вас были проблемы с завершением этого руководства.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-190">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="ce1b2-191">Бот не подключен к Teams</span><span class="sxs-lookup"><span data-stu-id="ce1b2-191">Bot isn't connected to Teams</span></span>


<span data-ttu-id="ce1b2-192">Если вы установили приложение, но бот не работает, убедитесь, что бот подключен к каналу службы Teams Azure [Bot. ](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ce1b2-192">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="ce1b2-193">Важно понимать, что это не то же самое, что канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="ce1b2-193">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="ce1b2-194">В этом случае канал — это способ подключения службы ботов Azure к Teams или другого поддерживаемого приложения связи Майкрософт или [сторонних разработчиков.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ce1b2-194">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="ce1b2-195">См. также</span><span class="sxs-lookup"><span data-stu-id="ce1b2-195">See also</span></span>

* [<span data-ttu-id="ce1b2-196">Основы бота</span><span class="sxs-lookup"><span data-stu-id="ce1b2-196">Bot basics</span></span>](../bots/bot-basics.md)
* [<span data-ttu-id="ce1b2-197">Создайте личную вкладку для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ce1b2-197">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
* [<span data-ttu-id="ce1b2-198">Узнайте, что Teams боты могут сделать с одним из наших образцов</span><span class="sxs-lookup"><span data-stu-id="ce1b2-198">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="ce1b2-199">Основы беседы для ботов</span><span class="sxs-lookup"><span data-stu-id="ce1b2-199">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="ce1b2-200">Рекомендации по дизайну</span><span class="sxs-lookup"><span data-stu-id="ce1b2-200">Design guidelines</span></span>](../bots/design/bots.md) 
* [<span data-ttu-id="ce1b2-201">Шаблоны пользовательского интерфейса, готовые к производству</span><span class="sxs-lookup"><span data-stu-id="ce1b2-201">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md)
* [<span data-ttu-id="ce1b2-202">Проверка подлинности ботов в Teams</span><span class="sxs-lookup"><span data-stu-id="ce1b2-202">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="ce1b2-203">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ce1b2-203">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="ce1b2-204">Создание бота без инструментария</span><span class="sxs-lookup"><span data-stu-id="ce1b2-204">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a><span data-ttu-id="ce1b2-205">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="ce1b2-205">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ce1b2-206">Создание расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="ce1b2-206">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
