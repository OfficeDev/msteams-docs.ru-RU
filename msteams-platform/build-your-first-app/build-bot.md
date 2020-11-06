---
title: Начало работы — Создание ленты
author: heath-hamilton
description: Быстро создайте робот Microsoft Teams с помощью набора инструментов Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 1229064ac6b7aab73c50048f0764c6a2353ab54a
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931743"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="ab747-103">Создание почтового робота для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ab747-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="ab747-104">В этом руководстве вы создадите базовое приложение для *ленты* .</span><span class="sxs-lookup"><span data-stu-id="ab747-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="ab747-105">Bot выступает в качестве посредника между пользователями Teams и веб-службой.</span><span class="sxs-lookup"><span data-stu-id="ab747-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="ab747-106">Люди могут общаться с программой-роботом, чтобы быстро получить сведения или инициировать рабочие процессы и задачи, выполняемые службой.</span><span class="sxs-lookup"><span data-stu-id="ab747-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="ab747-107">Ваше назначение</span><span class="sxs-lookup"><span data-stu-id="ab747-107">Your assignment</span></span>

<span data-ttu-id="ab747-108">Рабочая область создала приложение Teams, в котором используются [вкладки](../build-your-first-app/build-personal-tab.md) для отображения важных контактных сведений.</span><span class="sxs-lookup"><span data-stu-id="ab747-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="ab747-109">Например, сотрудники имеют быстрый доступ к номеру телефона службы поддержки.</span><span class="sxs-lookup"><span data-stu-id="ab747-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="ab747-110">Но не звонить, что делать, если пользователи могут обращаться в службу технической поддержки с помощью чатбот?</span><span class="sxs-lookup"><span data-stu-id="ab747-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="ab747-111">Ваш начальник попросит узнать, как быстро можно получить основной робот и запустить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="ab747-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="ab747-112">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="ab747-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ab747-113">Создание проекта приложения и Bot с помощью набора инструментов Microsoft Teams для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ab747-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="ab747-114">Определите некоторые конфигурации приложений и формирование шаблонов, относящихся к Боты</span><span class="sxs-lookup"><span data-stu-id="ab747-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="ab747-115">Локальное размещение приложения</span><span class="sxs-lookup"><span data-stu-id="ab747-115">Host an app locally</span></span>
> * <span data-ttu-id="ab747-116">Настройка почтового робота для Teams</span><span class="sxs-lookup"><span data-stu-id="ab747-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="ab747-117">Загрузка неопубликованных и тестирование ленты в Teams</span><span class="sxs-lookup"><span data-stu-id="ab747-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ab747-118">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="ab747-118">Before you begin</span></span>

<span data-ttu-id="ab747-119">Если вы еще не сделали это, убедитесь, что вы [знаете и установите необходимые компоненты для разработки Teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="ab747-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="ab747-120">1. Создайте проект приложения.</span><span class="sxs-lookup"><span data-stu-id="ab747-120">1. Create your app project</span></span>

<span data-ttu-id="ab747-121">Набор средств Microsoft Teams помогает настроить следующие компоненты для вашего приложения:</span><span class="sxs-lookup"><span data-stu-id="ab747-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="ab747-122">**Конфигурации приложений и формирование шаблонов,** относящиеся к Боты</span><span class="sxs-lookup"><span data-stu-id="ab747-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="ab747-123">**Bot** , автоматически регистрируемый в службе Microsoft Azure Bot</span><span class="sxs-lookup"><span data-stu-id="ab747-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="ab747-124">Если вы еще не создали проект приложения Teams, возможно, вам будет полезно выполнить приведенные [выше инструкции по](../build-your-first-app/build-and-run.md) более подробному объяснению проектов.</span><span class="sxs-lookup"><span data-stu-id="ab747-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
1. <span data-ttu-id="ab747-126">При появлении соответствующего запроса войдите в систему с помощью учетной записи разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="ab747-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="ab747-127">На экране **добавить возможности** выберите элемент **Bot** , а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ab747-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="ab747-128">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="ab747-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="ab747-129">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="ab747-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="ab747-130">Перейдите к разделу **Настройка Bot** и выберите **создать новый робот** , а затем **создайте регистрацию для ленты**.</span><span class="sxs-lookup"><span data-stu-id="ab747-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="ab747-131">В случае успеха новый робот будет иметь **зарегистрированное** состояние.</span><span class="sxs-lookup"><span data-stu-id="ab747-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="ab747-132">В нижней части экрана нажмите кнопку **Готово** и выберите расположение для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="ab747-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="ab747-133">2. определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="ab747-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="ab747-134">Многие конфигурации приложений и формирование шаблонов настраиваются автоматически при создании проекта с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="ab747-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="ab747-135">Рассмотрим основные компоненты для создания ленты.</span><span class="sxs-lookup"><span data-stu-id="ab747-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="ab747-136">Конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="ab747-136">App configurations</span></span>

<span data-ttu-id="ab747-137">Чтобы просмотреть или изменить конфигурации ленты, выберите **app Studio** в наборе инструментов и перейдите к **Боты**.</span><span class="sxs-lookup"><span data-stu-id="ab747-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="ab747-138">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="ab747-138">App scaffolding</span></span>

<span data-ttu-id="ab747-139">Формирование шаблонов приложений предоставляет `botActivityHandler.js` файл, расположенный в корневом каталоге проекта, для обработки действий ленты в Teams (например, как Bot реагирует на определенные сообщения, такие как "Hello").</span><span class="sxs-lookup"><span data-stu-id="ab747-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="ab747-140">3. Настройка безопасного туннеля для приложения</span><span class="sxs-lookup"><span data-stu-id="ab747-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="ab747-141">В целях тестирования давайте разместите свое приложение на локальном веб-сервере (порт 3978).</span><span class="sxs-lookup"><span data-stu-id="ab747-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="ab747-142">Если вы еще не сделали это, установите [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="ab747-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="ab747-143">В терминале запустите `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="ab747-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="ab747-144">Скопируйте URL-адрес HTTPS в выходных данных (например, `https://468b9ab725e9.ngrok.io` ), так как для Teams необходимы HTTPS-подключения.</span><span class="sxs-lookup"><span data-stu-id="ab747-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="ab747-145">При использовании этого URL-адреса Teams (для которых требуются HTTPS-подключения) смогут подключаться к месту размещения приложения ( `localhost` на порте 3978).</span><span class="sxs-lookup"><span data-stu-id="ab747-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="ab747-146">4. Настройка ленты</span><span class="sxs-lookup"><span data-stu-id="ab747-146">4. Configure your bot</span></span>

<span data-ttu-id="ab747-147">Чтобы использовать Bot в Teams, необходимо зарегистрировать его в службе Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="ab747-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="ab747-148">Счастливого Вам, это выполняется автоматически при настройке приложения с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="ab747-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="ab747-149">По-прежнему необходимо указать адрес конечной точки для получения и обработки сообщений пользователя (например, запросов), отправляемых в Bot.</span><span class="sxs-lookup"><span data-stu-id="ab747-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="ab747-150">Как правило, URL-адрес выглядит так `https://HOST_URL/api/messages` :</span><span class="sxs-lookup"><span data-stu-id="ab747-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="ab747-151">Вы можете быстро настроить его в наборе инструментов.</span><span class="sxs-lookup"><span data-stu-id="ab747-151">You can configure this quickly in the toolkit.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели действий, а затем выберите пункт **Открыть набор средств Microsoft Teams**.
1. <span data-ttu-id="ab747-153">Перейдите в **боты > существующие регистрации Bot** и выберите робот, созданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="ab747-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="ab747-154">В поле **адрес конечной точки Bot** введите URL-адрес ngrok (например,), на `https://468b9ab725e9.ngrok.io` котором размещается Bot и добавьте `/api/messages` к нему.</span><span class="sxs-lookup"><span data-stu-id="ab747-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Иллюстрация, на которой показано, как настроить URL-адрес конечной точки Bot в наборе инструментов Teams.":::

<span data-ttu-id="ab747-156">Ваш робот сможет отвечать на сообщения в Teams.</span><span class="sxs-lookup"><span data-stu-id="ab747-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="ab747-157">5. Построение и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="ab747-157">5. Build and run your app</span></span>

<span data-ttu-id="ab747-158">Вы настроили URL-адрес для размещения ленты и настроен для обработки сообщений.</span><span class="sxs-lookup"><span data-stu-id="ab747-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="ab747-159">Самое время заставить ваше приложение работать и работать.</span><span class="sxs-lookup"><span data-stu-id="ab747-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="ab747-160">В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .</span><span class="sxs-lookup"><span data-stu-id="ab747-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="ab747-161">Выполните команду `npm start` .</span><span class="sxs-lookup"><span data-stu-id="ab747-161">Run `npm start`.</span></span>

<span data-ttu-id="ab747-162">В случае успеха вы увидите следующее сообщение, указывающее на то, что Bot ожидает активности `localhost` :</span><span class="sxs-lookup"><span data-stu-id="ab747-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="ab747-163">6. Загрузка неопубликованных ваш Bot в Teams</span><span class="sxs-lookup"><span data-stu-id="ab747-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="ab747-164">С помощью программы Bot вы можете установить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="ab747-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="ab747-165">Если вы еще не неопубликованные приложение Teams до и не выпустили проблемы, выполните указанные ниже [действия](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="ab747-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="ab747-166">В Visual Studio Code нажмите клавишу **F5** , чтобы запустить веб-клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="ab747-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="ab747-167">В диалоговом окне Установка приложения нажмите кнопку " **Добавить** ".</span><span class="sxs-lookup"><span data-stu-id="ab747-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="ab747-168">(Вы можете добавить робота в канал или чат, но это не является более подправной стороны для проверки ленты в одном сеансе.)</span><span class="sxs-lookup"><span data-stu-id="ab747-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="ab747-169">7. Тестирование ленты</span><span class="sxs-lookup"><span data-stu-id="ab747-169">7. Test your bot</span></span>

<span data-ttu-id="ab747-170">Теперь скажите "Привет", чтобы приступить к развлечениям.</span><span class="sxs-lookup"><span data-stu-id="ab747-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="ab747-171">В поле создать отправьте `Hello` сообщение.</span><span class="sxs-lookup"><span data-stu-id="ab747-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="ab747-172">Ваш робот отправляется примерно следующим сообщениям.</span><span class="sxs-lookup"><span data-stu-id="ab747-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Снимок экрана, на котором показано, как пользователь наводит _OL_QUOTE_PLACEHOLDER_Hello_OL_QUOTE_PLACEHOLDER_ на робот команд и получает ответ.":::

## <a name="well-done"></a><span data-ttu-id="ab747-174">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="ab747-174">Well done</span></span>

<span data-ttu-id="ab747-175">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="ab747-175">Congratulations!</span></span> <span data-ttu-id="ab747-176">У вас есть простая пользовательская Командная ленты Teams, которая может общаться с пользователями один-к одному или в параметрах группы (каналы и сеансы).</span><span class="sxs-lookup"><span data-stu-id="ab747-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ab747-177">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="ab747-177">Troubleshooting</span></span>

<span data-ttu-id="ab747-178">Приведенные ниже сведения помогут вам устранить проблемы, связанные с выполнением этого руководства.</span><span class="sxs-lookup"><span data-stu-id="ab747-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="ab747-179">Bot не подключены к Teams</span><span class="sxs-lookup"><span data-stu-id="ab747-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="ab747-180">Если вы установили приложение, но Bot не работает, убедитесь, что он [подключен к *каналу* команд службы Azure Bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="ab747-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="ab747-181">Важно понимать, что это не то же самое, что и канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="ab747-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="ab747-182">В этом случае каналом является способ подключения службы Azure Bot к Teams или другому [поддерживаемому Microsoft или стороннему приложению для общения](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="ab747-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="ab747-183">Подробнее</span><span class="sxs-lookup"><span data-stu-id="ab747-183">Learn more</span></span>

* [<span data-ttu-id="ab747-184">Узнайте, что еще могут делать команды Боты Teams с одним из наших примеров.</span><span class="sxs-lookup"><span data-stu-id="ab747-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="ab747-185">Основы беседы для ботов</span><span class="sxs-lookup"><span data-stu-id="ab747-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="ab747-186">Односерверная проверка подлинности в Teams</span><span class="sxs-lookup"><span data-stu-id="ab747-186">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="ab747-187">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="ab747-187">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="ab747-188">Создание ленты без набора инструментов</span><span class="sxs-lookup"><span data-stu-id="ab747-188">Create a bot without the toolkit</span></span>](../bots/how-to/create-a-bot-for-teams.md)
