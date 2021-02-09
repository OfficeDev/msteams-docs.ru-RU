---
title: Начало работы — создание бота
author: heath-hamilton
description: Быстро создайте бот Microsoft Teams с помощью microsoft Teams набор средств.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 3e07c148e1b03431dc419a4e3679abac0229ff72
ms.sourcegitcommit: e08f309f62db2cf0f505f2aadfe728e5b46c17a5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/08/2021
ms.locfileid: "50140470"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="28c20-103">Создание бота для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="28c20-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="28c20-104">В этом руководстве  вы создадим базовое бот-приложение.</span><span class="sxs-lookup"><span data-stu-id="28c20-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="28c20-105">Бот действует как посредник между пользователями Teams и веб-службой.</span><span class="sxs-lookup"><span data-stu-id="28c20-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="28c20-106">Люди могут общаться с ботом, чтобы быстро получить информацию или инициировать рабочий процесс и задачи, выполняемые вашей службой.</span><span class="sxs-lookup"><span data-stu-id="28c20-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="28c20-107">Назначение</span><span class="sxs-lookup"><span data-stu-id="28c20-107">Your assignment</span></span>

<span data-ttu-id="28c20-108">На рабочем месте создано приложение Teams, использующее [вкладки](../build-your-first-app/build-personal-tab.md) для получения важных контактных данных.</span><span class="sxs-lookup"><span data-stu-id="28c20-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="28c20-109">Например, у коллег есть быстрый доступ к номеру телефона службы поддержки.</span><span class="sxs-lookup"><span data-stu-id="28c20-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="28c20-110">Но что делать, если бы люди могли обращаться в службу поддержки с помощью чат-робота?</span><span class="sxs-lookup"><span data-stu-id="28c20-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="28c20-111">Ваш начальник просит вас узнать, как быстро вы можете получить базовый бот для бесед в Teams.</span><span class="sxs-lookup"><span data-stu-id="28c20-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="28c20-112">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="28c20-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="28c20-113">Создание проекта приложения и бота с помощью microsoft Teams набор средств для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="28c20-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="28c20-114">Определение некоторых конфигураций приложений и скаолдинг, релевантный для ботов</span><span class="sxs-lookup"><span data-stu-id="28c20-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="28c20-115">Локальное приложение</span><span class="sxs-lookup"><span data-stu-id="28c20-115">Host an app locally</span></span>
> * <span data-ttu-id="28c20-116">Настройка бота для Teams</span><span class="sxs-lookup"><span data-stu-id="28c20-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="28c20-117">Загрузка неогрузки и тестирование бота в Teams</span><span class="sxs-lookup"><span data-stu-id="28c20-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="28c20-118">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="28c20-118">Before you begin</span></span>

<span data-ttu-id="28c20-119">Если вы еще не знаете и не установили необходимые условия для [разработки Teams.](build-first-app-overview.md#get-prerequisites)</span><span class="sxs-lookup"><span data-stu-id="28c20-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="28c20-120">1. Создайте проект приложения</span><span class="sxs-lookup"><span data-stu-id="28c20-120">1. Create your app project</span></span>

<span data-ttu-id="28c20-121">Microsoft Teams набор средств поможет вам настроить следующие компоненты для вашего приложения:</span><span class="sxs-lookup"><span data-stu-id="28c20-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="28c20-122">**Конфигурации приложений и скафолдинг,** релевантные для ботов</span><span class="sxs-lookup"><span data-stu-id="28c20-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="28c20-123">**Бот,** автоматически зарегистрированный в службе ботов Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="28c20-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="28c20-124">Если вы еще не создавали проект приложения Teams, возможно, вам будет полезно следовать этим инструкциям, чтобы подробнее объяснить проекты. [](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="28c20-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. В Visual Studio кода выберите **Microsoft Teams** в левой панели действий и выберите :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **"Создать новое приложение Teams".**
1. <span data-ttu-id="28c20-126">При запросе во sign in with your Microsoft 365 development account.</span><span class="sxs-lookup"><span data-stu-id="28c20-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="28c20-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span><span class="sxs-lookup"><span data-stu-id="28c20-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="28c20-128">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="28c20-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="28c20-129">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="28c20-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="28c20-130">Go to **Configure bot** and select **Create a new Bot** then Create Bot **Registration**.</span><span class="sxs-lookup"><span data-stu-id="28c20-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="28c20-131">В случае успеха новый бот будет иметь **зарегистрированный** статус.</span><span class="sxs-lookup"><span data-stu-id="28c20-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="28c20-132">Выберите **"Готово"** в нижней части экрана и выберите расположение для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="28c20-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="28c20-133">2. Определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="28c20-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="28c20-134">Большая часть конфигураций и скафаолдинга приложений автоматически заданная при создании проекта с помощью командной набор средств.</span><span class="sxs-lookup"><span data-stu-id="28c20-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="28c20-135">Рассмотрим основные компоненты для создания бота.</span><span class="sxs-lookup"><span data-stu-id="28c20-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="28c20-136">Конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="28c20-136">App configurations</span></span>

<span data-ttu-id="28c20-137">Чтобы просмотреть или обновить конфигурации бота, выберите **App Studio** в наборе средств и перейдите к **ботам.**</span><span class="sxs-lookup"><span data-stu-id="28c20-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="28c20-138">Скафаолдинг приложений</span><span class="sxs-lookup"><span data-stu-id="28c20-138">App scaffolding</span></span>

<span data-ttu-id="28c20-139">Скафолдинг приложения предоставляет файл, расположенный в корневом каталоге проекта, для обработки того, как бот обрабатывает действия в Teams (например, как бот реагирует на определенные сообщения, такие как `botActivityHandler.js` "Hello").</span><span class="sxs-lookup"><span data-stu-id="28c20-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="28c20-140">3. Настройка безопасного туннеля для приложения</span><span class="sxs-lookup"><span data-stu-id="28c20-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="28c20-141">Для тестирования разберем ваше приложение на локальном веб-сервере (порт 3978).</span><span class="sxs-lookup"><span data-stu-id="28c20-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="28c20-142">Если вы еще не сделали этого, установите [ngrok.](https://ngrok.com/download)</span><span class="sxs-lookup"><span data-stu-id="28c20-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="28c20-143">В терминале запустите `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="28c20-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="28c20-144">Скопируйте URL-адрес HTTPS в выходных данных (например, ),так как `https://468b9ab725e9.ngrok.io` Teams требует подключения HTTPS.</span><span class="sxs-lookup"><span data-stu-id="28c20-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="28c20-145">С помощью этого URL-адреса Teams (для которого требуются подключения ПО HTTPS) будет иметь туннель, в котором размещено приложение (через порт `localhost` 3978).</span><span class="sxs-lookup"><span data-stu-id="28c20-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="28c20-146">4. Настройте бота</span><span class="sxs-lookup"><span data-stu-id="28c20-146">4. Configure your bot</span></span>

<span data-ttu-id="28c20-147">Чтобы использовать бота в Teams, необходимо зарегистрировать его в службе ботов Azure.</span><span class="sxs-lookup"><span data-stu-id="28c20-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="28c20-148">Это делается автоматически при настройках приложения с помощью командной набор средств.</span><span class="sxs-lookup"><span data-stu-id="28c20-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="28c20-149">Вам по-прежнему необходимо указать адрес конечной точки для получения и обработки пользовательских сообщений (то есть запросов), отправленных боту.</span><span class="sxs-lookup"><span data-stu-id="28c20-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="28c20-150">Как правило, URL-адрес `https://HOST_URL/api/messages` выглядит.</span><span class="sxs-lookup"><span data-stu-id="28c20-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="28c20-151">Это можно быстро настроить в наборе средств.</span><span class="sxs-lookup"><span data-stu-id="28c20-151">You can configure this quickly in the toolkit.</span></span>

1. В Visual Studio code выберите **Microsoft Teams** в левой панели действий и :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: выберите команду **"Открыть Microsoft Teams набор средств.**
1. <span data-ttu-id="28c20-153">Перейдите **в > регистрации** существующих ботов и выберите бота, созданного во время установки.</span><span class="sxs-lookup"><span data-stu-id="28c20-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="28c20-154">В поле **адреса конечной точки бота** введите URL-адрес ngrok (например, url-адрес), в котором размещен бот, и `https://468b9ab725e9.ngrok.io` введите `/api/messages` его.</span><span class="sxs-lookup"><span data-stu-id="28c20-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Иллюстрация, показывающая, где можно настроить URL-адрес конечной точки бота в набор средств.":::

<span data-ttu-id="28c20-156">Бот сможет отвечать на сообщения в Teams.</span><span class="sxs-lookup"><span data-stu-id="28c20-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="28c20-157">5. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="28c20-157">5. Build and run your app</span></span>

<span data-ttu-id="28c20-158">Вы настроили URL-адрес для своего бота и настроили его для обработки сообщений.</span><span class="sxs-lookup"><span data-stu-id="28c20-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="28c20-159">Пора приумножите свое приложение к работе.</span><span class="sxs-lookup"><span data-stu-id="28c20-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="28c20-160">В терминале перейдите в корневой каталог проекта приложения и запустите `npm install` его.</span><span class="sxs-lookup"><span data-stu-id="28c20-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="28c20-161">Запустите `npm start` .</span><span class="sxs-lookup"><span data-stu-id="28c20-161">Run `npm start`.</span></span>

<span data-ttu-id="28c20-162">В случае успеха вы увидите следующее сообщение, указывающее, что ваш бот прослушивает действия на вашем `localhost` компьютере:</span><span class="sxs-lookup"><span data-stu-id="28c20-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="28c20-163">6. Загрузка нео sideload бота в Teams</span><span class="sxs-lookup"><span data-stu-id="28c20-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="28c20-164">С помощью бота вы можете установить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="28c20-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="28c20-165">Если вы еще не выгружали неогруженные приложения Teams и не могли с ним работать, следуйте [этим инструкциям.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="28c20-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="28c20-166">В Visual Studio Code нажмите клавишу **F5,** чтобы запустить веб-клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="28c20-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="28c20-167">В диалоговом окте "Установка приложения" выберите **"Добавить для меня".**</span><span class="sxs-lookup"><span data-stu-id="28c20-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="28c20-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span><span class="sxs-lookup"><span data-stu-id="28c20-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="28c20-169">7. Тестирование бота</span><span class="sxs-lookup"><span data-stu-id="28c20-169">7. Test your bot</span></span>

<span data-ttu-id="28c20-170">Теперь для интересной части: скажите "Hello" вашему боту.</span><span class="sxs-lookup"><span data-stu-id="28c20-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="28c20-171">В поле составить `Hello` сообщение.</span><span class="sxs-lookup"><span data-stu-id="28c20-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="28c20-172">Бот отвечает следующим сообщением:</span><span class="sxs-lookup"><span data-stu-id="28c20-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Снимок экрана: пользователь говорит &quot;Hello&quot; боту Teams и получает ответ.":::

## <a name="well-done"></a><span data-ttu-id="28c20-174">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="28c20-174">Well done</span></span>

<span data-ttu-id="28c20-175">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="28c20-175">Congratulations!</span></span> <span data-ttu-id="28c20-176">У вас есть базовый бот Teams, который может взаимодействовать с пользователями по одному или в параметрах группы (каналах и чатах).</span><span class="sxs-lookup"><span data-stu-id="28c20-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="28c20-177">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="28c20-177">Troubleshooting</span></span>

<span data-ttu-id="28c20-178">Следующие сведения могут помочь, если у вас были проблемы с выполнением этого руководства.</span><span class="sxs-lookup"><span data-stu-id="28c20-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="28c20-179">Бот не подключен к Teams</span><span class="sxs-lookup"><span data-stu-id="28c20-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="28c20-180">Если вы установили приложение, но бот не работает, убедитесь, что бот подключен к каналу Teams службы ботов [Azure. ](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="28c20-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="28c20-181">Важно понимать, что это не то же самое, что канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="28c20-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="28c20-182">В этом случае служба ботов Azure подключает бота к Teams или другому поддерживаемом [приложению Майкрософт](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)или стороннему приложению для связи.</span><span class="sxs-lookup"><span data-stu-id="28c20-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="28c20-183">Подробнее</span><span class="sxs-lookup"><span data-stu-id="28c20-183">Learn more</span></span>

* [<span data-ttu-id="28c20-184">Узнайте, что еще могут делать боты Teams с одним из наших примеров</span><span class="sxs-lookup"><span data-stu-id="28c20-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="28c20-185">Основы беседы для ботов</span><span class="sxs-lookup"><span data-stu-id="28c20-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* <span data-ttu-id="28c20-186">Следуйте [нашим рекомендациям по проектированию](../bots/design/bots.md) и создавайте [шаблоны](../concepts/design/design-teams-app-ui-templates.md) пользовательского интерфейса, готовые к выпуску, чтобы у вас было простое впечатление.</span><span class="sxs-lookup"><span data-stu-id="28c20-186">Follow our [design guidelines](../bots/design/bots.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="28c20-187">Проверка подлинности ботов в Teams</span><span class="sxs-lookup"><span data-stu-id="28c20-187">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="28c20-188">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="28c20-188">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="28c20-189">Создание бота без наборов средств</span><span class="sxs-lookup"><span data-stu-id="28c20-189">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)
