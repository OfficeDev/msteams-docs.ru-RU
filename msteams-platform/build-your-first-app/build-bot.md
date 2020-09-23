---
title: Создание ленты Teams
author: heath-hamilton
description: Узнайте, как создать робота для первого приложения Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: 7d3d1b63aace7fda971fb6ccaddddf631b4b2ad9
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210195"
---
# <a name="build-a-teams-bot"></a><span data-ttu-id="8aad0-103">Создание ленты Teams</span><span class="sxs-lookup"><span data-stu-id="8aad0-103">Build a Teams bot</span></span>

<span data-ttu-id="8aad0-104">В этом руководстве вы создадите базовое приложение для *ленты* .</span><span class="sxs-lookup"><span data-stu-id="8aad0-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="8aad0-105">Bot выступает в качестве посредника между пользователями Teams и веб-службой.</span><span class="sxs-lookup"><span data-stu-id="8aad0-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="8aad0-106">Люди могут общаться с программой-роботом, чтобы быстро получить сведения или инициировать рабочие процессы и задачи, выполняемые службой.</span><span class="sxs-lookup"><span data-stu-id="8aad0-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="8aad0-107">Ваше назначение</span><span class="sxs-lookup"><span data-stu-id="8aad0-107">Your assignment</span></span>

<span data-ttu-id="8aad0-108">На рабочем месте вы настроили важные контактные данные в Teams с помощью [вкладок](../build-your-first-app/build-personal-tab.md) .</span><span class="sxs-lookup"><span data-stu-id="8aad0-108">Your workplace has been using [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information in Teams.</span></span> <span data-ttu-id="8aad0-109">Например, сотрудники имеют быстрый доступ к номеру телефона службы поддержки.</span><span class="sxs-lookup"><span data-stu-id="8aad0-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="8aad0-110">Но не звонить, что делать, если пользователи могут обращаться в службу технической поддержки с помощью чатбот?</span><span class="sxs-lookup"><span data-stu-id="8aad0-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="8aad0-111">Ваш начальник попросит узнать, как быстро можно получить основной робот и запустить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="8aad0-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="8aad0-112">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="8aad0-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="8aad0-113">Создание проекта приложения и Bot с помощью набора инструментов Microsoft Teams для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8aad0-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="8aad0-114">Определение некоторых свойств манифеста приложения и формирование шаблонов, относящихся к Боты</span><span class="sxs-lookup"><span data-stu-id="8aad0-114">Identify some of the app manifest properties and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="8aad0-115">Локальное размещение приложения</span><span class="sxs-lookup"><span data-stu-id="8aad0-115">Host an app locally</span></span>
> * <span data-ttu-id="8aad0-116">Настройка почтового робота для Teams</span><span class="sxs-lookup"><span data-stu-id="8aad0-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="8aad0-117">Загрузка неопубликованных и тестирование ленты в Teams</span><span class="sxs-lookup"><span data-stu-id="8aad0-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8aad0-118">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="8aad0-118">Before you begin</span></span>

<span data-ttu-id="8aad0-119">Если вы еще не сделали это, убедитесь, что вы [знаете и установите необходимые компоненты для разработки Teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="8aad0-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="create-your-app-project"></a><span data-ttu-id="8aad0-120">Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="8aad0-120">Create your app project</span></span>

<span data-ttu-id="8aad0-121">Набор средств Microsoft Teams помогает настроить следующие компоненты для вашего приложения:</span><span class="sxs-lookup"><span data-stu-id="8aad0-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="8aad0-122">**Манифест приложения и формирование шаблонов,** относящиеся к Боты</span><span class="sxs-lookup"><span data-stu-id="8aad0-122">**App manifest and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="8aad0-123">**Bot** , автоматически регистрируемый в службе Microsoft Azure Bot</span><span class="sxs-lookup"><span data-stu-id="8aad0-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="8aad0-124">Если вы еще не создали проект приложения Teams, возможно, вам будет полезно выполнить приведенные [выше инструкции по](../build-your-first-app/build-and-run.md) более подробному объяснению проектов.</span><span class="sxs-lookup"><span data-stu-id="8aad0-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
1. <span data-ttu-id="8aad0-126">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="8aad0-126">Enter a name for your Teams app.</span></span> <span data-ttu-id="8aad0-127">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="8aad0-127">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="8aad0-128">На экране **добавить возможности** выберите элемент **Bot** , а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8aad0-128">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="8aad0-129">Выберите **создать новый робот** **и войдите в систему,** используя учетную запись Microsoft 365 для разработки.</span><span class="sxs-lookup"><span data-stu-id="8aad0-129">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span><br/>
:::image type="content" source="../assets/images/build-your-first-app/vsc-create-bot.png" alt-text="Иллюстрация, на которой показано, как с помощью набора инструментов Teams войти в свою учетную запись Microsoft 365, чтобы создать новый робот.":::
1. <span data-ttu-id="8aad0-131">Сохраните идентификатор и пароль почтового робота (это необходимо сделать чуть позже).</span><span class="sxs-lookup"><span data-stu-id="8aad0-131">Store your bot ID and password (you need this a little later).</span></span>
1. <span data-ttu-id="8aad0-132">Необязательно Введите настраиваемое имя для Bot и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="8aad0-132">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="8aad0-133">(Помните, что это имя для ленты, а не имя уже указанного приложения Teams.)</span><span class="sxs-lookup"><span data-stu-id="8aad0-133">(Remember, this is the name for your bot and not the name of the Teams app you already specified.)</span></span>
1. <span data-ttu-id="8aad0-134">В нижней части экрана нажмите кнопку **Готово** , чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="8aad0-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="8aad0-135">Определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="8aad0-135">Identify relevant app project components</span></span>

<span data-ttu-id="8aad0-136">Большинство манифестов и шаблонов приложений настраиваются автоматически при создании проекта с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="8aad0-136">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="8aad0-137">Рассмотрим основные компоненты для создания ленты.</span><span class="sxs-lookup"><span data-stu-id="8aad0-137">Let's look at the main components for building a bot.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="8aad0-138">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="8aad0-138">App manifest</span></span>

<span data-ttu-id="8aad0-139">В следующем фрагменте кода из манифеста приложения ( `manifest.json` файл в каталоге проекта `.publish` ) показаны свойства и значения по умолчанию, относящиеся к Боты.</span><span class="sxs-lookup"><span data-stu-id="8aad0-139">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to bots.</span></span>

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

<span data-ttu-id="8aad0-140">Пока что давайте рассмотрим следующие обязательные свойства.</span><span class="sxs-lookup"><span data-stu-id="8aad0-140">For now, let's just focus on the following required properties.</span></span> <span data-ttu-id="8aad0-141">(Обратитесь к полному списку поддерживаемых [`bots`](../resources/schema/manifest-schema.md#bots) свойств.)</span><span class="sxs-lookup"><span data-stu-id="8aad0-141">(See the full list of supported [`bots`](../resources/schema/manifest-schema.md#bots) properties.)</span></span>

* <span data-ttu-id="8aad0-142">`botId`: Идентификатор созданного робота, созданного вами с помощью настройки проекта.</span><span class="sxs-lookup"><span data-stu-id="8aad0-142">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="8aad0-143">(Хранимая в `{botId0}` , вы можете найти фактический идентификатор в `Development.env` .)</span><span class="sxs-lookup"><span data-stu-id="8aad0-143">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="8aad0-144">`scopes`: Указывает, доступна ли для ленты появляющиеся `personal` `groupchat` `team` контексты, или (например, каналы).</span><span class="sxs-lookup"><span data-stu-id="8aad0-144">`scopes`: Specifies if your bot is available in `personal`, `groupchat`, or `team` (i.e., channel) contexts.</span></span>
* <span data-ttu-id="8aad0-145">`commands`: Доступны команды, которые пользователи могут отправлять на ваш робот.</span><span class="sxs-lookup"><span data-stu-id="8aad0-145">`commands`: Available commands users can send to your bot.</span></span>
* <span data-ttu-id="8aad0-146">`title`: Имя команды Bot, отображаемое в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="8aad0-146">`title`: Bot command name that displays in the Teams client.</span></span>
* <span data-ttu-id="8aad0-147">`description`: Краткое описание или пример синтаксиса и аргументов, которые помогают пользователям определить, что делает команда Bot.</span><span class="sxs-lookup"><span data-stu-id="8aad0-147">`description`: A short description or example of the syntax and arguments to help users understand what a bot command does.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="8aad0-148">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="8aad0-148">App scaffolding</span></span>

<span data-ttu-id="8aad0-149">Формирование шаблонов приложений предоставляет `botActivityHandler.js` файл, расположенный в корневом каталоге проекта, для обработки действий ленты в Teams (например, как Bot реагирует на определенные сообщения, такие как "Hello").</span><span class="sxs-lookup"><span data-stu-id="8aad0-149">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

<span data-ttu-id="8aad0-150">В `.env` файле, также в корневом каталоге, ХРАНЯТСЯ идентификатор и пароль Bot.</span><span class="sxs-lookup"><span data-stu-id="8aad0-150">The `.env` file, also in the root directory, stores your bot ID and password.</span></span>

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="8aad0-151">Настройка безопасного туннеля для приложения</span><span class="sxs-lookup"><span data-stu-id="8aad0-151">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="8aad0-152">В целях тестирования давайте разместите Bot на локальном веб-сервере (порт 3978).</span><span class="sxs-lookup"><span data-stu-id="8aad0-152">For testing purposes, let's host your bot on a local web server (port 3978).</span></span>

1. <span data-ttu-id="8aad0-153">В терминале запустите `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="8aad0-153">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="8aad0-154">Скопируйте URL-адрес HTTPS в выходных данных, так как teams требует HTTPS-подключения.</span><span class="sxs-lookup"><span data-stu-id="8aad0-154">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="8aad0-155">В `.publish` каталоге откройте `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="8aad0-155">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="8aad0-156">Замените `baseUrl0` значение скопированным URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="8aad0-156">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="8aad0-157">(Например, замените `baseUrl0=http://localhost:3000` на `baseUrl0=https://85528b2b3ca5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="8aad0-157">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="8aad0-158">Манифест приложения указывает на место размещения ленты.</span><span class="sxs-lookup"><span data-stu-id="8aad0-158">Your app manifest is pointing to where you're hosting the bot.</span></span>

## <a name="configuring-your-bot"></a><span data-ttu-id="8aad0-159">Настройка ленты</span><span class="sxs-lookup"><span data-stu-id="8aad0-159">Configuring your bot</span></span>

<span data-ttu-id="8aad0-160">Чтобы использовать Bot в Teams, необходимо зарегистрировать его в службе Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="8aad0-160">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="8aad0-161">Счастливого Вам, это выполняется автоматически при настройке приложения с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="8aad0-161">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

### <a name="specify-your-bot-id-and-password"></a><span data-ttu-id="8aad0-162">Указание идентификатора и пароля почтового робота</span><span class="sxs-lookup"><span data-stu-id="8aad0-162">Specify your bot ID and password</span></span>

<span data-ttu-id="8aad0-163">Когда ваш Bot зарегистрирован в службе Azure Bot, ему назначается идентификатор и пароль, о которых должно знать ваше приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="8aad0-163">When your bot is registered with the Azure Bot Service, it's assigned an ID and password that your Teams app must know about.</span></span>

1. <span data-ttu-id="8aad0-164">Нахождение идентификатора и пароля ленты, сохраненных во время установки набора средств.</span><span class="sxs-lookup"><span data-stu-id="8aad0-164">Locate the bot ID and password you stored during toolkit setup.</span></span>
1. <span data-ttu-id="8aad0-165">Откройте файл в корневом каталоге `.env` .</span><span class="sxs-lookup"><span data-stu-id="8aad0-165">In your root directory, open the `.env` file.</span></span>
1. <span data-ttu-id="8aad0-166">Добавьте идентификатор и пароль для почтового робота `BotId` и `BotPassword` соответственно.</span><span class="sxs-lookup"><span data-stu-id="8aad0-166">Add your bot ID and password to `BotId` and `BotPassword`, respectively.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="8aad0-167">Добавление адреса конечной точки Bot</span><span class="sxs-lookup"><span data-stu-id="8aad0-167">Add the bot endpoint address</span></span>

<span data-ttu-id="8aad0-168">Необходимо указать URL-адрес конечной точки для получения и обработки сообщений пользователя (например, запросов), отправляемых в Bot.</span><span class="sxs-lookup"><span data-stu-id="8aad0-168">You must specify an endpoint URL to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="8aad0-169">Как правило, URL-адрес выглядит так `https://HOST_URL/api/messages` :</span><span class="sxs-lookup"><span data-stu-id="8aad0-169">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="8aad0-170">Это можно сделать быстро в наборе инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="8aad0-170">You can configure this quickly in the Teams Toolkit.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели действий, а затем выберите пункт **Открыть набор средств Microsoft Teams**.
1. <span data-ttu-id="8aad0-172">Перейдите к элементу **управления Bot > существующих регистраций ленты** и выберите элемент управления Bot, созданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="8aad0-172">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="8aad0-173">В поле **адрес конечной точки Bot** введите локальный веб-сервер, на котором размещается Bot ( `baseUrl10` значение), и добавьте `/api/messages` к нему.</span><span class="sxs-lookup"><span data-stu-id="8aad0-173">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot (`baseUrl10` value) and append `/api/messages` to it.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Иллюстрация, на которой показано, как настроить URL-адрес конечной точки Bot в наборе инструментов Teams.":::

<span data-ttu-id="8aad0-175">Ваш робот сможет отвечать на сообщения в Teams.</span><span class="sxs-lookup"><span data-stu-id="8aad0-175">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="8aad0-176">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="8aad0-176">Run your app</span></span>

<span data-ttu-id="8aad0-177">Вы настроили URL-адрес для размещения ленты и настроен для обработки сообщений.</span><span class="sxs-lookup"><span data-stu-id="8aad0-177">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="8aad0-178">Время для начала работы с роботом.</span><span class="sxs-lookup"><span data-stu-id="8aad0-178">It's time to get your bot up and running.</span></span>

1. <span data-ttu-id="8aad0-179">В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .</span><span class="sxs-lookup"><span data-stu-id="8aad0-179">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="8aad0-180">Выполните команду `npm start` .</span><span class="sxs-lookup"><span data-stu-id="8aad0-180">Run `npm start`.</span></span>

<span data-ttu-id="8aad0-181">В случае успеха вы увидите нечто вроде приведенного ниже сообщения, указывающего на то, что Bot выполняет прослушивание действий в `localhost` :</span><span class="sxs-lookup"><span data-stu-id="8aad0-181">If successful, you see something like the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="sideload-your-bot-in-teams"></a><span data-ttu-id="8aad0-182">Загрузка неопубликованных ленты в Teams</span><span class="sxs-lookup"><span data-stu-id="8aad0-182">Sideload your bot in Teams</span></span>

<span data-ttu-id="8aad0-183">С помощью программы Bot вы можете установить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="8aad0-183">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="8aad0-184">Если вы еще не неопубликованные приложение Teams до и не выпустили проблемы, выполните указанные ниже [действия](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="8aad0-184">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="8aad0-185">Выполните вход в клиент Teams с учетной записью, позволяющей выполнять загрузку неопубликованных приложений.</span><span class="sxs-lookup"><span data-stu-id="8aad0-185">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="8aad0-186">Выберите **приложения**, а затем нажмите кнопку **Отправить пользовательское приложение**.</span><span class="sxs-lookup"><span data-stu-id="8aad0-186">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="8aad0-187">Перейдите в папку проекта приложения `.publish` и выберите `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="8aad0-187">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="8aad0-188">В модальном окне установки нажмите кнопку **Добавить** , чтобы установить приложение.</span><span class="sxs-lookup"><span data-stu-id="8aad0-188">In the install modal, select **Add** to install your app.</span></span>

## <a name="test-your-bot"></a><span data-ttu-id="8aad0-189">Тестирование ленты</span><span class="sxs-lookup"><span data-stu-id="8aad0-189">Test your bot</span></span>

<span data-ttu-id="8aad0-190">Теперь, когда у вас есть забавная часть, скажите "Привет" в роботе в одном сеансе.</span><span class="sxs-lookup"><span data-stu-id="8aad0-190">Now for the fun part: Let's say "Hello" to your bot in a one-on-one chat.</span></span>

1. В группе Teams выберите в левой части элемент **Дополнительно** :::image type="icon" source="../assets/icons/teams-client-more.png"::: .
1. <span data-ttu-id="8aad0-192">Перейдите к простому неопубликованные и выберите его.</span><span class="sxs-lookup"><span data-stu-id="8aad0-192">Locate and choose the bot you just sideloaded.</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/bot-teams-access.png" alt-text="Иллюстрация, на которой показано, как получить доступ к панели роботов в Teams.":::
1. <span data-ttu-id="8aad0-194">В поле создать отправьте `Hello` сообщение.</span><span class="sxs-lookup"><span data-stu-id="8aad0-194">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="8aad0-195">Ваш робот отправляется примерно следующим сообщениям.</span><span class="sxs-lookup"><span data-stu-id="8aad0-195">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Снимок экрана, на котором показано, как пользователь наводит "Hello" на робот команд и получает ответ.":::

## <a name="well-done"></a><span data-ttu-id="8aad0-197">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="8aad0-197">Well done</span></span>

<span data-ttu-id="8aad0-198">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="8aad0-198">Congratulations!</span></span> <span data-ttu-id="8aad0-199">У вас есть простая пользовательская Командная ленты Teams, которая может общаться с пользователями один-к одному или в параметрах группы (каналы и сеансы).</span><span class="sxs-lookup"><span data-stu-id="8aad0-199">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8aad0-200">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="8aad0-200">Troubleshooting</span></span>

<span data-ttu-id="8aad0-201">Приведенные ниже сведения помогут вам устранить проблемы, связанные с выполнением этого руководства.</span><span class="sxs-lookup"><span data-stu-id="8aad0-201">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="8aad0-202">Не удается установить набор средств</span><span class="sxs-lookup"><span data-stu-id="8aad0-202">Toolkit setup fails</span></span>

<span data-ttu-id="8aad0-203">Когда вы настраиваете проект приложения с помощью набора инструментов Teams, вы получаете сообщение об ошибке после выбора параметра **создать новый элемент Bot** и входа в систему с помощью учетной записи разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="8aad0-203">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="8aad0-204">Это может быть проблема проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8aad0-204">This could be an authentication issue.</span></span> <span data-ttu-id="8aad0-205">Выполните следующие действия, чтобы завершить настройку проекта.</span><span class="sxs-lookup"><span data-stu-id="8aad0-205">Follow these steps to finish setting up your project.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели действий и нажмите **выйти**.
1. <span data-ttu-id="8aad0-207">Снова пройдите процесс настройки, выполнив вход в систему с той же учетной записью и создав новый элемент Bot.</span><span class="sxs-lookup"><span data-stu-id="8aad0-207">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="8aad0-208">Bot не подключены к Teams</span><span class="sxs-lookup"><span data-stu-id="8aad0-208">Bot isn't connected to Teams</span></span>

<span data-ttu-id="8aad0-209">Если вы установили приложение, но Bot не работает, убедитесь, что он [подключен к *каналу*команд службы Azure Bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="8aad0-209">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="8aad0-210">Важно понимать, что это не то же самое, что и канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="8aad0-210">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="8aad0-211">В этом случае каналом является способ подключения службы Azure Bot к Teams или другому [поддерживаемому Microsoft или стороннему приложению для общения](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="8aad0-211">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="8aad0-212">Подробнее</span><span class="sxs-lookup"><span data-stu-id="8aad0-212">Learn more</span></span>

* [<span data-ttu-id="8aad0-213">Узнайте, что еще могут делать команды Боты Teams с одним из наших примеров.</span><span class="sxs-lookup"><span data-stu-id="8aad0-213">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="8aad0-214">Основы беседы для ботов</span><span class="sxs-lookup"><span data-stu-id="8aad0-214">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="8aad0-215">Односерверная проверка подлинности в Teams</span><span class="sxs-lookup"><span data-stu-id="8aad0-215">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="8aad0-216">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="8aad0-216">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="8aad0-217">Создание ленты без набора инструментов</span><span class="sxs-lookup"><span data-stu-id="8aad0-217">Create a bot without the toolkit</span></span>](../bots/how-to/create-a-bot-for-teams.md)
