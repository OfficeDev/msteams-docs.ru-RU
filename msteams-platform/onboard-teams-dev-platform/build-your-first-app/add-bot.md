---
title: Создать бота для Teams
author: heath-hamilton
description: Узнайте, как создать Bot в первом приложении Microsoft Teams.
ms.author: lajanuar
ms.date: 08/31/2020
ms.topic: tutorial
ms.openlocfilehash: f1307bcc7bb864ddfa97b9297f34fa4f7d5fcb0d
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964778"
---
# <a name="create-a-bot-for-teams"></a><span data-ttu-id="0e802-103">Создать бота для Teams</span><span class="sxs-lookup"><span data-stu-id="0e802-103">Create a bot for Teams</span></span>

<span data-ttu-id="0e802-104">В этом руководстве вы создадите базовое приложение для *ленты* .</span><span class="sxs-lookup"><span data-stu-id="0e802-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="0e802-105">Bot выступает в качестве посредника между пользователями Teams и веб-службой.</span><span class="sxs-lookup"><span data-stu-id="0e802-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="0e802-106">Люди могут общаться с программой-роботом, чтобы быстро получить сведения или инициировать рабочие процессы и задачи, выполняемые службой.</span><span class="sxs-lookup"><span data-stu-id="0e802-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="0e802-107">Ваше назначение</span><span class="sxs-lookup"><span data-stu-id="0e802-107">Your assignment</span></span>

<span data-ttu-id="0e802-108">На рабочем месте вы настроили важные контактные данные в Teams с помощью [вкладок](../build-your-first-app/add-personal-tab.md) .</span><span class="sxs-lookup"><span data-stu-id="0e802-108">Your workplace has been using [tabs](../build-your-first-app/add-personal-tab.md) to surface important contact information in Teams.</span></span> <span data-ttu-id="0e802-109">Например, сотрудники имеют быстрый доступ к номеру телефона службы поддержки.</span><span class="sxs-lookup"><span data-stu-id="0e802-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="0e802-110">Но не звонить, что делать, если пользователи могут обращаться в службу технической поддержки с помощью чатбот?</span><span class="sxs-lookup"><span data-stu-id="0e802-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="0e802-111">Ваш начальник попросит узнать, как быстро можно получить основной робот и запустить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="0e802-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="0e802-112">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="0e802-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="0e802-113">Создание проекта приложения и Bot с помощью набора инструментов Microsoft Teams для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0e802-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="0e802-114">Определите свойства манифеста приложения и некоторые шаблоны формирования шаблонов, относящиеся к Боты</span><span class="sxs-lookup"><span data-stu-id="0e802-114">Identify the app manifest properties and some of the scaffolding relevant to bots</span></span>
> * <span data-ttu-id="0e802-115">Размещение ленты на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="0e802-115">Host a bot locally</span></span>
> * <span data-ttu-id="0e802-116">Настройка почтового робота для Teams</span><span class="sxs-lookup"><span data-stu-id="0e802-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="0e802-117">Загрузка неопубликованных и тестирование ленты в Teams</span><span class="sxs-lookup"><span data-stu-id="0e802-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0e802-118">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="0e802-118">Before you begin</span></span>

<span data-ttu-id="0e802-119">Если вы еще не сделали это, настройте [учетную запись](building-real-world-app.md#set-up-your-development-account) Microsoft 365 Development и [средства Teams](building-real-world-app.md#install-your-development-tools).</span><span class="sxs-lookup"><span data-stu-id="0e802-119">If you haven't yet, set up your Microsoft 365 development [account](building-real-world-app.md#set-up-your-development-account) and [Teams app tools](building-real-world-app.md#install-your-development-tools).</span></span>

## <a name="create-your-app-project-and-bot"></a><span data-ttu-id="0e802-120">Создание проекта приложения и ленты</span><span class="sxs-lookup"><span data-stu-id="0e802-120">Create your app project and bot</span></span>

<span data-ttu-id="0e802-121">Набор средств Microsoft Teams помогает настроить следующие компоненты для вашего приложения:</span><span class="sxs-lookup"><span data-stu-id="0e802-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="0e802-122">**Проект приложения**: включает манифест приложения и формирование шаблонов, относящихся к Боты</span><span class="sxs-lookup"><span data-stu-id="0e802-122">**App project**: Includes the app manifest and scaffolding relevant to bots</span></span>
* <span data-ttu-id="0e802-123">**Bot**: настраивает новый Bot и регистрирует его в службе Microsoft Azure Bot</span><span class="sxs-lookup"><span data-stu-id="0e802-123">**Bot**: Configures a new bot and registers it with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="0e802-124">Если вы еще не создали проект приложения Teams, возможно, вам будет полезно выполнить приведенные [выше инструкции по](../build-your-first-app/build-and-run.md) более подробному объяснению проектов.</span><span class="sxs-lookup"><span data-stu-id="0e802-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
1. <span data-ttu-id="0e802-126">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="0e802-126">Enter a name for your Teams app.</span></span> <span data-ttu-id="0e802-127">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="0e802-127">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="0e802-128">На экране **добавить возможности** выберите элемент **Bot** , а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0e802-128">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="0e802-129">Выберите **создать новый робот** **и войдите в систему,** используя учетную запись Microsoft 365 для разработки.</span><span class="sxs-lookup"><span data-stu-id="0e802-129">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span><br/>
:::image type="content" source="../doc-links/images/vsc-create-bot.png" alt-text="Иллюстрация, на которой показано, как с помощью набора инструментов Teams войти в свою учетную запись Microsoft 365, чтобы создать новый робот.":::
1. <span data-ttu-id="0e802-131">Необязательно Введите настраиваемое имя для Bot и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="0e802-131">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="0e802-132">(Помните, что это имя для ленты, а не имя уже указанного приложения Teams.)</span><span class="sxs-lookup"><span data-stu-id="0e802-132">(Remember, this is the name for your bot and not the name of the Teams app you already specified.)</span></span>
1. <span data-ttu-id="0e802-133">В нижней части экрана нажмите кнопку **Готово** , чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="0e802-133">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="0e802-134">Определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="0e802-134">Identify relevant app project components</span></span>

<span data-ttu-id="0e802-135">Большинство манифестов и шаблонов приложений настраиваются автоматически при создании проекта с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="0e802-135">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="0e802-136">Рассмотрим основные компоненты для создания ленты.</span><span class="sxs-lookup"><span data-stu-id="0e802-136">Let's look at the main components for building a bot.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="0e802-137">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="0e802-137">App manifest</span></span>

<span data-ttu-id="0e802-138">В следующем фрагменте кода из манифеста приложения ( `manifest.json` файл в каталоге проекта `.publish` ) показаны свойства и значения по умолчанию, относящиеся к Боты.</span><span class="sxs-lookup"><span data-stu-id="0e802-138">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to bots.</span></span>

```JSON
    "bots": [
        {
            "botId": "{botId0}",
            "scopes": [
                "personal",
                "groupchat",
                "team"
            ],
            "supportsFiles": false,
            "isNotificationOnly": false,
            "commandLists": [
                {
                    "scopes": [
                        "personal",
                        "groupchat",
                        "team"
                    ],
                    "commands": [
                        {
                            "title": "Hello",
                            "description": "Sends a hello message and @mention the sender"
                        }
                    ]
                }
            ]
        }
    ],
```

<span data-ttu-id="0e802-139">Пока что давайте рассмотрим следующие обязательные свойства.</span><span class="sxs-lookup"><span data-stu-id="0e802-139">For now, let's just focus on the following required properties.</span></span> <span data-ttu-id="0e802-140">(Обратитесь к полному списку поддерживаемых [`bots`](../../resources/schema/manifest-schema.md#bots) свойств.)</span><span class="sxs-lookup"><span data-stu-id="0e802-140">(See the full list of supported [`bots`](../../resources/schema/manifest-schema.md#bots) properties.)</span></span>

* <span data-ttu-id="0e802-141">`botId`: Идентификатор созданного робота, созданного вами с помощью настройки проекта.</span><span class="sxs-lookup"><span data-stu-id="0e802-141">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="0e802-142">(Хранимая в `{botId0}` , вы можете найти фактический идентификатор в `Development.env` .)</span><span class="sxs-lookup"><span data-stu-id="0e802-142">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="0e802-143">`scopes`: Указывает, доступна ли для ленты появляющиеся `personal` `groupchat` `team` контексты, или (например, каналы).</span><span class="sxs-lookup"><span data-stu-id="0e802-143">`scopes`: Specifies if your bot is available in `personal`, `groupchat`, or `team` (i.e., channel) contexts.</span></span>
* <span data-ttu-id="0e802-144">`commands`: Доступны команды, которые пользователи могут отправлять на ваш робот.</span><span class="sxs-lookup"><span data-stu-id="0e802-144">`commands`: Available commands users can send to your bot.</span></span>
* <span data-ttu-id="0e802-145">`title`: Имя команды Bot пользователи видят в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="0e802-145">`title`: A bot command name users see in the Teams client.</span></span>
* <span data-ttu-id="0e802-146">`description`: Краткое описание или пример синтаксиса и аргументов, которые помогают пользователям определить, что делает команда Bot.</span><span class="sxs-lookup"><span data-stu-id="0e802-146">`description`: A short description or example of the syntax and arguments to help users understand what a bot command does.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="0e802-147">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="0e802-147">App scaffolding</span></span>

<span data-ttu-id="0e802-148">Формирование шаблонов приложений предоставляет `botActivityHandler.js` файл, расположенный в корневом каталоге проекта, для обработки действий ленты в Teams (например, как Bot реагирует на определенные сообщения, такие как "Hello").</span><span class="sxs-lookup"><span data-stu-id="0e802-148">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="0e802-149">Настройка безопасного туннеля для приложения</span><span class="sxs-lookup"><span data-stu-id="0e802-149">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="0e802-150">В целях тестирования давайте разместите Bot на локальном веб-сервере (порт 3978).</span><span class="sxs-lookup"><span data-stu-id="0e802-150">For testing purposes, let's host your bot on a local web server (port 3978).</span></span>

1. <span data-ttu-id="0e802-151">В терминале запустите `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="0e802-151">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="0e802-152">Скопируйте URL-адрес HTTPS в выходных данных, так как teams требует HTTPS-подключения.</span><span class="sxs-lookup"><span data-stu-id="0e802-152">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="0e802-153">В `.publish` каталоге откройте `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="0e802-153">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="0e802-154">Замените `baseUrl0` значение скопированным URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="0e802-154">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="0e802-155">(Например, замените `baseUrl0=http://localhost:3000` на `baseUrl0=https://85528b2b3ca5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="0e802-155">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="0e802-156">Манифест приложения указывает на место размещения ленты.</span><span class="sxs-lookup"><span data-stu-id="0e802-156">Your app manifest is pointing to where you're hosting the bot.</span></span>

## <a name="configuring-your-bot"></a><span data-ttu-id="0e802-157">Настройка ленты</span><span class="sxs-lookup"><span data-stu-id="0e802-157">Configuring your bot</span></span>

<span data-ttu-id="0e802-158">Чтобы использовать Bot в Teams, необходимо зарегистрировать его в службе Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="0e802-158">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="0e802-159">Счастливого Вам, это выполняется автоматически при настройке приложения с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="0e802-159">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="0e802-160">Добавление адреса конечной точки Bot</span><span class="sxs-lookup"><span data-stu-id="0e802-160">Add the bot endpoint address</span></span>

<span data-ttu-id="0e802-161">Необходимо указать URL-адрес конечной точки для получения и обработки сообщений пользователя (например, запросов), отправляемых в Bot.</span><span class="sxs-lookup"><span data-stu-id="0e802-161">You must specify an endpoint URL to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="0e802-162">Как правило, URL-адрес выглядит так `https://HOST_URL/api/messages` :</span><span class="sxs-lookup"><span data-stu-id="0e802-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="0e802-163">Это можно сделать быстро в наборе инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="0e802-163">You can configure this quickly in the Teams Toolkit.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: на левой панели действий, а затем выберите пункт **Открыть набор средств Microsoft Teams**.
1. <span data-ttu-id="0e802-165">Перейдите к элементу **управления Bot > существующих регистраций ленты** и выберите элемент управления Bot, созданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="0e802-165">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="0e802-166">В поле **адрес конечной точки Bot** введите локальный веб-сервер, на котором размещается Bot, и добавьте `/api/messages` к нему.</span><span class="sxs-lookup"><span data-stu-id="0e802-166">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot and append `/api/messages` to it.</span></span>

    :::image type="content" source="../doc-links/images/bot-config-endpoint-url.png" alt-text="Иллюстрация, на которой показано, как настроить URL-адрес конечной точки Bot в наборе инструментов Teams.":::

<span data-ttu-id="0e802-168">Ваш робот сможет отвечать на сообщения в Teams.</span><span class="sxs-lookup"><span data-stu-id="0e802-168">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="0e802-169">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="0e802-169">Run your app</span></span>

<span data-ttu-id="0e802-170">Вы настроили URL-адрес для размещения ленты и настроен для обработки сообщений.</span><span class="sxs-lookup"><span data-stu-id="0e802-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="0e802-171">Время для начала работы с роботом.</span><span class="sxs-lookup"><span data-stu-id="0e802-171">It's time to get your bot up and running.</span></span>

1. <span data-ttu-id="0e802-172">В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .</span><span class="sxs-lookup"><span data-stu-id="0e802-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="0e802-173">Выполните команду `npm start` .</span><span class="sxs-lookup"><span data-stu-id="0e802-173">Run `npm start`.</span></span>

<span data-ttu-id="0e802-174">В случае успеха вы увидите нечто вроде приведенного ниже сообщения, указывающего на то, что Bot выполняет прослушивание действий в `localhost` :</span><span class="sxs-lookup"><span data-stu-id="0e802-174">If successful, you see something like the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="sideload-your-bot-in-teams"></a><span data-ttu-id="0e802-175">Загрузка неопубликованных ленты в Teams</span><span class="sxs-lookup"><span data-stu-id="0e802-175">Sideload your bot in Teams</span></span>

<span data-ttu-id="0e802-176">С помощью программы Bot вы можете установить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="0e802-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="0e802-177">Если вы еще не неопубликованные приложение Teams до и не выпустили проблемы, выполните указанные ниже [действия](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="0e802-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="0e802-178">Выполните вход в клиент Teams с учетной записью, позволяющей выполнять загрузку неопубликованных приложений.</span><span class="sxs-lookup"><span data-stu-id="0e802-178">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="0e802-179">Выберите **приложения**, а затем нажмите кнопку **Отправить пользовательское приложение**.</span><span class="sxs-lookup"><span data-stu-id="0e802-179">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="0e802-180">Перейдите в папку проекта приложения `.publish` и выберите `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="0e802-180">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="0e802-181">В модальном окне установки нажмите кнопку **Добавить** , чтобы установить приложение.</span><span class="sxs-lookup"><span data-stu-id="0e802-181">In the install modal, select **Add** to install your app.</span></span>

## <a name="test-your-bot"></a><span data-ttu-id="0e802-182">Тестирование ленты</span><span class="sxs-lookup"><span data-stu-id="0e802-182">Test your bot</span></span>

<span data-ttu-id="0e802-183">Теперь, когда у вас есть забавная часть, скажите "Привет" в роботе в одном сеансе.</span><span class="sxs-lookup"><span data-stu-id="0e802-183">Now for the fun part: Let's say "Hello" to your bot in a one-on-one chat.</span></span>

1. В группе Teams выберите в левой части элемент **Дополнительно** :::image type="icon" source="../doc-links/images/teams-client-more.png"::: .
1. <span data-ttu-id="0e802-185">Перейдите к нужному элементу Bot и выберите только что неопубликованные.</span><span class="sxs-lookup"><span data-stu-id="0e802-185">Locate and select the bot you just sideloaded.</span></span><br/>
   :::image type="content" source="../doc-links/images/bot-teams-access.png" alt-text="Иллюстрация, на которой показано, как получить доступ к панели роботов в Teams.":::
1. <span data-ttu-id="0e802-187">В поле создать отправьте `Hello` сообщение.</span><span class="sxs-lookup"><span data-stu-id="0e802-187">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="0e802-188">Ваш робот отправляется примерно следующим сообщениям.</span><span class="sxs-lookup"><span data-stu-id="0e802-188">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../doc-links/images/contoso-chatbot.png" alt-text="Снимок экрана, на котором показано, как пользователь наводит сообщение "Hello" на робот команд и получает ответ обратно.":::

> [!NOTE]
> <span data-ttu-id="0e802-190">Если вы вносите изменения в код после проверки ленты (например, обновление `botActivityHandler.js` ), необходимо повторно запустить приложение, чтобы увидеть изменения, отраженные в Teams.</span><span class="sxs-lookup"><span data-stu-id="0e802-190">If you make code changes after testing your bot—for example, you update `botActivityHandler.js`—you must run your app again to see those changes reflected in Teams.</span></span>

## <a name="well-done"></a><span data-ttu-id="0e802-191">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="0e802-191">Well done</span></span>

<span data-ttu-id="0e802-192">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="0e802-192">Congratulations!</span></span> <span data-ttu-id="0e802-193">У вас есть простая пользовательская Командная ленты Teams, которая может общаться с пользователями один-к одному или в параметрах группы (каналы и сеансы).</span><span class="sxs-lookup"><span data-stu-id="0e802-193">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0e802-194">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="0e802-194">Troubleshooting</span></span>

<span data-ttu-id="0e802-195">Приведенные ниже сведения помогут вам устранить проблемы, связанные с выполнением этого руководства.</span><span class="sxs-lookup"><span data-stu-id="0e802-195">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="0e802-196">Не удается установить набор средств</span><span class="sxs-lookup"><span data-stu-id="0e802-196">Toolkit setup fails</span></span>

<span data-ttu-id="0e802-197">Когда вы настраиваете проект приложения с помощью набора инструментов Teams, вы получаете сообщение об ошибке после выбора параметра **создать новый элемент Bot** и входа в систему с помощью учетной записи разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="0e802-197">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="0e802-198">Это может быть проблема проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0e802-198">This could be an authentication issue.</span></span> <span data-ttu-id="0e802-199">Выполните следующие действия, чтобы завершить настройку проекта.</span><span class="sxs-lookup"><span data-stu-id="0e802-199">Follow these steps to finish setting up your project.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: на левой панели действий и нажмите **выйти**.
1. <span data-ttu-id="0e802-201">Снова пройдите процесс настройки, выполнив вход в систему с той же учетной записью и создав новый элемент Bot.</span><span class="sxs-lookup"><span data-stu-id="0e802-201">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="0e802-202">Bot не подключены к Teams</span><span class="sxs-lookup"><span data-stu-id="0e802-202">Bot isn't connected to Teams</span></span>

<span data-ttu-id="0e802-203">Если вы установили приложение, но Bot не работает, убедитесь, что он [подключен к *каналу*команд службы Azure Bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="0e802-203">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="0e802-204">Важно понимать, что это не то же самое, что и канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="0e802-204">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="0e802-205">В этом случае каналом является способ подключения службы Azure Bot к Teams или другому [поддерживаемому Microsoft или стороннему приложению для общения](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="0e802-205">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="0e802-206">Подробнее</span><span class="sxs-lookup"><span data-stu-id="0e802-206">Learn more</span></span>

* [<span data-ttu-id="0e802-207">Узнайте, какие другие возможности Teams Боты могут делать с одним из наших примеров (GitHub).</span><span class="sxs-lookup"><span data-stu-id="0e802-207">See what else Teams bots can do with one of our samples (GitHub)</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="0e802-208">Основы беседы для ботов</span><span class="sxs-lookup"><span data-stu-id="0e802-208">Bot conversation basics</span></span>](../../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="0e802-209">Односерверная проверка подлинности в Teams</span><span class="sxs-lookup"><span data-stu-id="0e802-209">Bot authentication in Teams</span></span>](../../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="0e802-210">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0e802-210">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
