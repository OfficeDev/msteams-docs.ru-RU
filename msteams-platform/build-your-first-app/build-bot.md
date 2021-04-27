---
title: Начало работы — сборка бота
author: heath-hamilton
description: Быстро создайте бот Microsoft Teams с помощью microsoft Teams набор средств.
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 5dfbfa05d2f1e36bbc14bd929cb2592303081522
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020002"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="b60f5-103">Создание бота для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b60f5-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="b60f5-104">В этом учебнике будет *построено* базовое бот-приложение.</span><span class="sxs-lookup"><span data-stu-id="b60f5-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="b60f5-105">Бот выступает в качестве посредника между пользователями Teams и веб-службой.</span><span class="sxs-lookup"><span data-stu-id="b60f5-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="b60f5-106">Люди могут общаться с ботом, чтобы быстро получить информацию или инициировать рабочий процесс и задачи, выполняемые вашей службой.</span><span class="sxs-lookup"><span data-stu-id="b60f5-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="b60f5-107">Назначение</span><span class="sxs-lookup"><span data-stu-id="b60f5-107">Your assignment</span></span>

<span data-ttu-id="b60f5-108">На рабочем месте создано приложение Teams, которое использует [вкладки для](../build-your-first-app/build-personal-tab.md) получения важных контактных данных.</span><span class="sxs-lookup"><span data-stu-id="b60f5-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="b60f5-109">Например, у коллег есть быстрый доступ к номеру телефона службы поддержки.</span><span class="sxs-lookup"><span data-stu-id="b60f5-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="b60f5-110">Но вместо вызова, что делать, если люди могли связаться с помощью службы поддержки с помощью чат-бота?</span><span class="sxs-lookup"><span data-stu-id="b60f5-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="b60f5-111">Ваш босс просит вас посмотреть, как быстро вы можете получить базовый разговорный бот и запуск в Teams.</span><span class="sxs-lookup"><span data-stu-id="b60f5-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="b60f5-112">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="b60f5-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="b60f5-113">Создание проекта приложения и бота с помощью microsoft Teams набор средств для Visual Studio кода</span><span class="sxs-lookup"><span data-stu-id="b60f5-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="b60f5-114">Определение некоторых конфигураций приложений и строительных лесов, соответствующих ботам</span><span class="sxs-lookup"><span data-stu-id="b60f5-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="b60f5-115">Локальное хост-приложение</span><span class="sxs-lookup"><span data-stu-id="b60f5-115">Host an app locally</span></span>
> * <span data-ttu-id="b60f5-116">Настройка бота для Teams</span><span class="sxs-lookup"><span data-stu-id="b60f5-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="b60f5-117">Боковая загрузка и тестирование бота в Teams</span><span class="sxs-lookup"><span data-stu-id="b60f5-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b60f5-118">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="b60f5-118">Before you begin</span></span>

<span data-ttu-id="b60f5-119">Если еще нет, убедитесь, что вы понимаете и установите необходимые условия [для разработки Teams.](build-first-app-overview.md#get-prerequisites)</span><span class="sxs-lookup"><span data-stu-id="b60f5-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="b60f5-120">1. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="b60f5-120">1. Create your app project</span></span>

<span data-ttu-id="b60f5-121">Программа Microsoft Teams набор средств позволяет настроить следующие компоненты для приложения:</span><span class="sxs-lookup"><span data-stu-id="b60f5-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="b60f5-122">**Конфигурации приложений и леса, соответствующие** ботам</span><span class="sxs-lookup"><span data-stu-id="b60f5-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="b60f5-123">**Бот,** автоматически зарегистрированный в службе Microsoft Azure Bot</span><span class="sxs-lookup"><span data-stu-id="b60f5-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="b60f5-124">Если вы еще не создали проект приложения Teams, может [](../build-your-first-app/build-and-run.md) оказаться полезным выполнять эти инструкции, которые подробно объясняют проекты.</span><span class="sxs-lookup"><span data-stu-id="b60f5-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. В Visual Studio коде выберите **Microsoft Teams** в левой панели действий и создайте новое приложение :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams.**
1. <span data-ttu-id="b60f5-126">При запросе впишитесь в учетную запись разработки Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="b60f5-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="b60f5-127">На экране **Добавить возможности** выберите **Bot** then **Next**.</span><span class="sxs-lookup"><span data-stu-id="b60f5-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="b60f5-128">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="b60f5-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="b60f5-129">(Это имя по умолчанию для вашего приложения, а также имя каталога проектов приложений на локальной машине.)</span><span class="sxs-lookup"><span data-stu-id="b60f5-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="b60f5-130">Перейдите **к Настройке бота** и **выберите Создать новый бот,** а затем создать **регистрацию бота.**</span><span class="sxs-lookup"><span data-stu-id="b60f5-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="b60f5-131">В случае успешной работы новый бот будет иметь **зарегистрированный** статус.</span><span class="sxs-lookup"><span data-stu-id="b60f5-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="b60f5-132">Выберите **Готово** в нижней части экрана и выберите расположение для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="b60f5-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="b60f5-133">2. Определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="b60f5-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="b60f5-134">Большая часть конфигураций приложений и строительных лесов создается автоматически при создании проекта с командной набор средств.</span><span class="sxs-lookup"><span data-stu-id="b60f5-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="b60f5-135">Рассмотрим основные компоненты для создания бота.</span><span class="sxs-lookup"><span data-stu-id="b60f5-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="b60f5-136">Конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="b60f5-136">App configurations</span></span>

<span data-ttu-id="b60f5-137">Чтобы просмотреть или обновить конфигурации бота, выберите **App Studio** в наборе инструментов и перейдите к **ботам.**</span><span class="sxs-lookup"><span data-stu-id="b60f5-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="b60f5-138">Строительные леса приложений</span><span class="sxs-lookup"><span data-stu-id="b60f5-138">App scaffolding</span></span>

<span data-ttu-id="b60f5-139">Строительные леса приложений предоставляют файл, расположенный в корневом каталоге проекта, для обработки действий бота в Teams (например, как бот реагирует на определенные сообщения, такие как `botActivityHandler.js` "Hello").</span><span class="sxs-lookup"><span data-stu-id="b60f5-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="b60f5-140">3. Настройка безопасного туннеля в приложении</span><span class="sxs-lookup"><span data-stu-id="b60f5-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="b60f5-141">Для тестирования давайте разберем ваше приложение на локальном веб-сервере (порт 3978).</span><span class="sxs-lookup"><span data-stu-id="b60f5-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="b60f5-142">Если вы еще не сделали этого, установите [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="b60f5-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="b60f5-143">В терминале запустите `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="b60f5-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="b60f5-144">Скопируйте URL-адрес HTTPS в выходе (например, ), так как `https://468b9ab725e9.ngrok.io` Teams требует подключений HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b60f5-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="b60f5-145">С помощью этого URL-адреса Teams (для которой требуются подключения HTTPS) смогут пройдите туннель туда, где размещено ваше приложение (в `localhost` порту 3978).</span><span class="sxs-lookup"><span data-stu-id="b60f5-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="b60f5-146">4. Настройка бота</span><span class="sxs-lookup"><span data-stu-id="b60f5-146">4. Configure your bot</span></span>

<span data-ttu-id="b60f5-147">Чтобы использовать бот в Teams, необходимо зарегистрировать его в службе Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="b60f5-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="b60f5-148">К счастью для вас, это делается автоматически при настройках приложения с помощью набор средств.</span><span class="sxs-lookup"><span data-stu-id="b60f5-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="b60f5-149">Для получения и обработки сообщений пользователей (например, запросов), отправленных боту, необходимо указать адрес конечной точки.</span><span class="sxs-lookup"><span data-stu-id="b60f5-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="b60f5-150">Как правило, URL-адрес выглядит `https://HOST_URL/api/messages` как .</span><span class="sxs-lookup"><span data-stu-id="b60f5-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="b60f5-151">Это можно быстро настроить в наборе инструментов.</span><span class="sxs-lookup"><span data-stu-id="b60f5-151">You can configure this quickly in the toolkit.</span></span>

1. В Visual Studio коде выберите **Microsoft Teams** в левой панели действий и выберите Open Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **набор средств**.
1. <span data-ttu-id="b60f5-153">Перейдите **к ботам > существующие регистрации** ботов и выберите бот, созданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="b60f5-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="b60f5-154">В поле **адресов конечной точки** бота введите URL-адрес ngrok (например, ), где вы размещены бот и `https://468b9ab725e9.ngrok.io` приложение к `/api/messages` ней.</span><span class="sxs-lookup"><span data-stu-id="b60f5-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="На рисунке показывая, где можно настроить URL-адрес конечной точки бота в командной набор средств.":::

<span data-ttu-id="b60f5-156">Ваш бот сможет отвечать на сообщения в Teams.</span><span class="sxs-lookup"><span data-stu-id="b60f5-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="b60f5-157">5. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="b60f5-157">5. Build and run your app</span></span>

<span data-ttu-id="b60f5-158">Вы настроили URL-адрес для хост-бота и настроили его для обработки сообщений.</span><span class="sxs-lookup"><span data-stu-id="b60f5-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="b60f5-159">Пришло время, чтобы ваше приложение было запущено.</span><span class="sxs-lookup"><span data-stu-id="b60f5-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="b60f5-160">В терминале перейдите в корневой каталог проекта приложения и запустите `npm install` .</span><span class="sxs-lookup"><span data-stu-id="b60f5-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="b60f5-161">Запуск `npm start` .</span><span class="sxs-lookup"><span data-stu-id="b60f5-161">Run `npm start`.</span></span>

<span data-ttu-id="b60f5-162">В случае успеха вы увидите следующее сообщение, указывающее на то, что ваш бот прослушивает действия в `localhost` вашем :</span><span class="sxs-lookup"><span data-stu-id="b60f5-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="b60f5-163">6. Боковой загрузки бота в Teams</span><span class="sxs-lookup"><span data-stu-id="b60f5-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="b60f5-164">При запуске бота его можно установить в Teams.</span><span class="sxs-lookup"><span data-stu-id="b60f5-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="b60f5-165">Если вы еще не перегружали приложение Teams до и не могли решить проблемы, следуйте [этим инструкциям.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="b60f5-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="b60f5-166">В Visual Studio коде нажмите **клавишу F5,** чтобы запустить веб-клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="b60f5-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="b60f5-167">В диалоговом окте установке приложения выберите **Добавить для меня**.</span><span class="sxs-lookup"><span data-stu-id="b60f5-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="b60f5-168">(Можно добавить бот в канал или чат, но другим менее навязчиво тестировать бота в чате один на один.)</span><span class="sxs-lookup"><span data-stu-id="b60f5-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="b60f5-169">7. Проверка бота</span><span class="sxs-lookup"><span data-stu-id="b60f5-169">7. Test your bot</span></span>

<span data-ttu-id="b60f5-170">Теперь для интересной части: Давайте скажем "Hello" для вашего бота.</span><span class="sxs-lookup"><span data-stu-id="b60f5-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="b60f5-171">В окне составить отправьте `Hello` сообщение.</span><span class="sxs-lookup"><span data-stu-id="b60f5-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="b60f5-172">Бот отвечает следующим сообщением.</span><span class="sxs-lookup"><span data-stu-id="b60f5-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Снимок экрана, на котором пользователь скажет &quot;Привет&quot; боту Teams и будет получать ответ.":::

## <a name="well-done"></a><span data-ttu-id="b60f5-174">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="b60f5-174">Well done</span></span>

<span data-ttu-id="b60f5-175">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b60f5-175">Congratulations!</span></span> <span data-ttu-id="b60f5-176">У вас есть базовый бот Teams, который может общаться с пользователями один на один или в групповых настройках (каналы и чаты).</span><span class="sxs-lookup"><span data-stu-id="b60f5-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b60f5-177">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="b60f5-177">Troubleshooting</span></span>

<span data-ttu-id="b60f5-178">Следующие сведения могут помочь, если у вас были проблемы с завершением этого руководства.</span><span class="sxs-lookup"><span data-stu-id="b60f5-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="b60f5-179">Бот не подключен к Teams</span><span class="sxs-lookup"><span data-stu-id="b60f5-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="b60f5-180">Если вы установили приложение, но бот не работает, убедитесь, что бот подключен к каналу [Teams службы ](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="b60f5-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="b60f5-181">Важно понимать, что это не то же самое, что канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="b60f5-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="b60f5-182">В этом случае канал — это способ подключения службы Azure Bot к Teams или другому поддерживаемом приложению майкрософт или сторонних [коммуникаций.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="b60f5-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="b60f5-183">Подробнее</span><span class="sxs-lookup"><span data-stu-id="b60f5-183">Learn more</span></span>

* [<span data-ttu-id="b60f5-184">Узнайте, что еще могут сделать боты Teams с одним из наших образцов</span><span class="sxs-lookup"><span data-stu-id="b60f5-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="b60f5-185">Основы беседы для ботов</span><span class="sxs-lookup"><span data-stu-id="b60f5-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* <span data-ttu-id="b60f5-186">Следуйте [нашим рекомендациям по проектированию](../bots/design/bots.md) и создайте с помощью готовых к производству шаблонов [пользовательского](../concepts/design/design-teams-app-ui-templates.md) интерфейса для создания бесшовного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b60f5-186">Follow our [design guidelines](../bots/design/bots.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="b60f5-187">Проверка подлинности ботов в Teams</span><span class="sxs-lookup"><span data-stu-id="b60f5-187">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="b60f5-188">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b60f5-188">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="b60f5-189">Создание бота без инструментария</span><span class="sxs-lookup"><span data-stu-id="b60f5-189">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)
