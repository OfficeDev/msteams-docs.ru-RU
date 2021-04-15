---
title: Начало работы — создание расширения обмена сообщениями
author: heath-hamilton
description: Быстро создайте расширение обмена сообщениями Microsoft Teams с помощью набор средств.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 09e851820314efd3dc114b926a0111603cac18a4
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696880"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="38805-103">Создание расширения обмена сообщениями для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="38805-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="38805-104">Существует два типа расширений обмена *сообщениями* Teams: [команды поиска](../messaging-extensions/how-to/search-commands/define-search-command.md) и [команды действий.](../messaging-extensions/how-to/action-commands/define-action-command.md)</span><span class="sxs-lookup"><span data-stu-id="38805-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="38805-105">В этом уроке будет создаваться команда поиска *(также* известная как расширение обмена сообщениями на основе *поиска),* которая является ярлыком для поиска внешнего контента и совместного использования его в Teams.</span><span class="sxs-lookup"><span data-stu-id="38805-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="38805-106">Пользователи могут получать доступ к командам поиска из [командного или командного окна Teams.](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="38805-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="38805-107">Назначение</span><span class="sxs-lookup"><span data-stu-id="38805-107">Your assignment</span></span>

<span data-ttu-id="38805-108">Отдел поддержки организации общается с пользователями через Teams, но билеты находятся в отдельной системе.</span><span class="sxs-lookup"><span data-stu-id="38805-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="38805-109">Это означает, что сотрудники службы поддержки должны постоянно ходить между приложениями.</span><span class="sxs-lookup"><span data-stu-id="38805-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="38805-110">Вы изучите, как уменьшить этот объем переключения контекста, создав простое расширение обмена сообщениями на основе поиска для Teams.</span><span class="sxs-lookup"><span data-stu-id="38805-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="38805-111">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="38805-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="38805-112">Создание бота расширения проекта приложения и обмена сообщениями с помощью microsoft Teams набор средств для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="38805-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="38805-113">Определение конфигураций приложений и некоторых строительных лесов, соответствующих расширению обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="38805-113">Identify the app configurations and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="38805-114">Локальное хост-приложение</span><span class="sxs-lookup"><span data-stu-id="38805-114">Host an app locally</span></span>
> * <span data-ttu-id="38805-115">Настройка бота для расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="38805-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="38805-116">Боковая загрузка и тестирование расширения обмена сообщениями в Teams</span><span class="sxs-lookup"><span data-stu-id="38805-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="38805-117">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="38805-117">Before you begin</span></span>

<span data-ttu-id="38805-118">Если еще нет, убедитесь, что вы понимаете и установите необходимые условия [для разработки Teams.](build-first-app-overview.md#get-prerequisites)</span><span class="sxs-lookup"><span data-stu-id="38805-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="38805-119">1. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="38805-119">1. Create your app project</span></span>

<span data-ttu-id="38805-120">Программа Microsoft Teams набор средств позволяет настроить следующие компоненты для расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="38805-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="38805-121">**Конфигурации приложений и леса,** соответствующие расширениям обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="38805-121">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="38805-122">**Бот** для расширения обмена сообщениями, который автоматически зарегистрирован в службе Microsoft Azure Bot</span><span class="sxs-lookup"><span data-stu-id="38805-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="38805-123">Если вы еще не создали проект приложения Teams, может [](../build-your-first-app/build-and-run.md) оказаться полезным выполнять эти инструкции, которые подробно объясняют проекты.</span><span class="sxs-lookup"><span data-stu-id="38805-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. В Visual Studio коде выберите **Microsoft Teams** в левой панели действий и создайте новое приложение :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams.**
1. <span data-ttu-id="38805-125">При запросе впишитесь в учетную запись разработки Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="38805-125">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="38805-126">На экране **Добавить возможности** выберите расширение обмена **сообщениями затем** **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38805-126">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="38805-127">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="38805-127">Enter a name for your Teams app.</span></span> <span data-ttu-id="38805-128">(Это имя по умолчанию для вашего приложения, а также имя каталога проектов приложений на локальной машине.)</span><span class="sxs-lookup"><span data-stu-id="38805-128">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="38805-129">На экране **расширения настройки обмена сообщениями** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="38805-129">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="38805-130">Выберите только **параметр На основе** поиска для типа расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="38805-130">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="38805-131">Выберите **Создать новый бот,** а **затем создать регистрацию бота.**</span><span class="sxs-lookup"><span data-stu-id="38805-131">Select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="38805-132">В случае успешной работы новый бот будет иметь **зарегистрированный** статус.</span><span class="sxs-lookup"><span data-stu-id="38805-132">If successful, your new bot will have a **Registered** status.</span></span>
    1. <span data-ttu-id="38805-133">На данный момент выберите **нет** для параметра "Нет" для разгрузки ссылки.</span><span class="sxs-lookup"><span data-stu-id="38805-133">For now, select **No** for the link unfurling option.</span></span>
1. <span data-ttu-id="38805-134">Выберите **Готово** в нижней части экрана, чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="38805-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="38805-135">2. Определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="38805-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="38805-136">Большая часть конфигураций приложений и строительных лесов создается автоматически при создании проекта с командной набор средств.</span><span class="sxs-lookup"><span data-stu-id="38805-136">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="38805-137">Конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="38805-137">App configurations</span></span>

<span data-ttu-id="38805-138">Чтобы просмотреть или обновить конфигурации расширения обмена сообщениями, выберите **App Studio** в наборе инструментов и перейдите к **расширениям обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="38805-138">To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="38805-139">Строительные леса приложений</span><span class="sxs-lookup"><span data-stu-id="38805-139">App scaffolding</span></span>

<span data-ttu-id="38805-140">Строительные леса приложений предоставляют файл, расположенный в корневом каталоге проекта, для обработки того, как расширение обмена сообщениями (или технически бот расширения обмена сообщениями) отвечает на поисковые запросы `botActivityHandler.js` в Teams. [](#4-configure-the-bot-for-your-messaging-extension)</span><span class="sxs-lookup"><span data-stu-id="38805-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="38805-141">3. Настройка безопасного туннеля в приложении</span><span class="sxs-lookup"><span data-stu-id="38805-141">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="38805-142">В целях тестирования разберем расширение обмена сообщениями на локальном веб-сервере (порт 3978).</span><span class="sxs-lookup"><span data-stu-id="38805-142">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="38805-143">Если вы еще не сделали этого, установите [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="38805-143">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="38805-144">В терминале запустите `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="38805-144">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="38805-145">Скопируйте URL-адрес HTTPS в выходе (например, ), так как `https://468b9ab725e9.ngrok.io` Teams требует подключений HTTPS.</span><span class="sxs-lookup"><span data-stu-id="38805-145">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="38805-146">С помощью этого URL-адреса Teams (для которой требуются подключения HTTPS) смогут пройдите туннель туда, где размещено ваше приложение (в `localhost` порту 3978).</span><span class="sxs-lookup"><span data-stu-id="38805-146">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="38805-147">4. Настройка бота для расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="38805-147">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="38805-148">Расширения обмена сообщениями используют боты для отправки и обработки запросов пользователей из Teams в вашу службу.</span><span class="sxs-lookup"><span data-stu-id="38805-148">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="38805-149">Бот должен быть зарегистрирован в службе Azure Bot Service, что было сделано при настройках приложения с помощью teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="38805-149">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="38805-150">Для получения и обработки поисковых запросов в расширении обмена сообщениями необходимо указать URL-адрес конечной точки бота.</span><span class="sxs-lookup"><span data-stu-id="38805-150">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="38805-151">Как правило, URL-адрес выглядит `https://HOST_URL/api/messages` как .</span><span class="sxs-lookup"><span data-stu-id="38805-151">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="38805-152">Это можно быстро настроить в наборе инструментов.</span><span class="sxs-lookup"><span data-stu-id="38805-152">You can configure this quickly in the toolkit.</span></span>

1. В Visual Studio коде выберите **Microsoft Teams** в левой панели действий и выберите Open Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **набор средств**.
1. <span data-ttu-id="38805-154">Перейдите **к ботам > существующие регистрации** ботов и выберите бот, созданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="38805-154">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="38805-155">В поле **адресов конечной точки** бота введите URL-адрес ngrok (например, ), где вы размещены бот и `https://468b9ab725e9.ngrok.io` приложение к `/api/messages` ней.</span><span class="sxs-lookup"><span data-stu-id="38805-155">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

<span data-ttu-id="38805-156">Ваш бот сможет обрабатывать запросы в расширении обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="38805-156">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="38805-157">5. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="38805-157">5. Build and run your app</span></span>

<span data-ttu-id="38805-158">Вы настроили URL-адрес для расширения обмена сообщениями и настроили его для обработки поиска.</span><span class="sxs-lookup"><span data-stu-id="38805-158">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="38805-159">Пришло время, чтобы ваше приложение было запущено.</span><span class="sxs-lookup"><span data-stu-id="38805-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="38805-160">В терминале перейдите в корневой каталог проекта приложения и запустите `npm install` .</span><span class="sxs-lookup"><span data-stu-id="38805-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="38805-161">Запуск `npm start` .</span><span class="sxs-lookup"><span data-stu-id="38805-161">Run `npm start`.</span></span>

<span data-ttu-id="38805-162">В случае успеха вы увидите следующее сообщение, указывающее, что служба расширения обмена сообщениями прослушивает действия в `localhost` вашем :</span><span class="sxs-lookup"><span data-stu-id="38805-162">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="38805-163">6. Sideload your messaging extension in Teams</span><span class="sxs-lookup"><span data-stu-id="38805-163">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="38805-164">При запуске расширения обмена сообщениями его можно установить в Teams.</span><span class="sxs-lookup"><span data-stu-id="38805-164">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="38805-165">Если вы еще не перегружали приложение Teams до и не могли решить проблемы, следуйте [этим инструкциям.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="38805-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="38805-166">В Visual Studio коде нажмите **клавишу F5,** чтобы запустить веб-клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="38805-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="38805-167">В диалоговом окте установке приложения выберите **Добавить для меня**.</span><span class="sxs-lookup"><span data-stu-id="38805-167">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="38805-168">7. Проверьте расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="38805-168">7. Test your messaging extension</span></span>

<span data-ttu-id="38805-169">Узнайте, как работают расширения обмена сообщениями в чате Teams.</span><span class="sxs-lookup"><span data-stu-id="38805-169">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="38805-170">Запустите новый чат.</span><span class="sxs-lookup"><span data-stu-id="38805-170">Start a new chat.</span></span> В окне составить выберите **Больше** и выберите приложение расширения обмена сообщениями, которое :::image type="icon" source="../assets/icons/teams-client-more.png"::: вы только что загружены.
1. <span data-ttu-id="38805-172">Попробуйте найти что-то (например, **Билеты).**</span><span class="sxs-lookup"><span data-stu-id="38805-172">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="38805-173">Если приложение работает, вы увидите пример результатов поиска (вы можете добавить свои собственные позже).</span><span class="sxs-lookup"><span data-stu-id="38805-173">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Снимок экрана, показывающий, как в поле &quot;Команды&quot; используется расширение обмена сообщениями на основе поиска.":::

## <a name="well-done"></a><span data-ttu-id="38805-175">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="38805-175">Well done</span></span>

<span data-ttu-id="38805-176">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="38805-176">Congratulations!</span></span> <span data-ttu-id="38805-177">У вас есть базовое расширение обмена сообщениями Teams, настроенное для поиска внешнего контента в окне составить или команду.</span><span class="sxs-lookup"><span data-stu-id="38805-177">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38805-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="38805-178">Next steps</span></span>

<span data-ttu-id="38805-179">См. следующие страницы для продолжения и создания полноцельного расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="38805-179">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="38805-180">[Определите команды поиска,](../messaging-extensions/how-to/search-commands/define-search-command.md) которые имеют отношение к вашей службе.</span><span class="sxs-lookup"><span data-stu-id="38805-180">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="38805-181">Настройка службы для [реагирования на поиск пользователей.](../messaging-extensions/how-to/search-commands/respond-to-search.md)</span><span class="sxs-lookup"><span data-stu-id="38805-181">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="38805-182">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="38805-182">Troubleshooting</span></span>

<span data-ttu-id="38805-183">Следующие сведения могут помочь, если у вас были проблемы с завершением этого руководства.</span><span class="sxs-lookup"><span data-stu-id="38805-183">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="38805-184">Бот не подключен к Teams</span><span class="sxs-lookup"><span data-stu-id="38805-184">Bot isn't connected to Teams</span></span>

<span data-ttu-id="38805-185">Если приложение установлено, но оно не работает, убедитесь, что бот расширения обмена сообщениями подключен к каналу [Teams службы ](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="38805-185">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="38805-186">Важно понимать, что это не то же самое, что канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="38805-186">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="38805-187">В этом случае канал — это способ подключения службы Azure Bot к Teams или другому поддерживаемом приложению майкрософт или сторонних [коммуникаций.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="38805-187">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="38805-188">Подробнее</span><span class="sxs-lookup"><span data-stu-id="38805-188">Learn more</span></span>

* [<span data-ttu-id="38805-189">Включить функцию разгрузки ссылок</span><span class="sxs-lookup"><span data-stu-id="38805-189">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* <span data-ttu-id="38805-190">Следуйте [нашим рекомендациям по проектированию](../messaging-extensions/design/messaging-extension-design.md) и создайте с помощью готовых к производству шаблонов [пользовательского](../concepts/design/design-teams-app-ui-templates.md) интерфейса для создания бесшовного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="38805-190">Follow our [design guidelines](../messaging-extensions/design/messaging-extension-design.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="38805-191">Добавление проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="38805-191">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="38805-192">Создание расширения обмена сообщениями на основе действий</span><span class="sxs-lookup"><span data-stu-id="38805-192">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="38805-193">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="38805-193">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)

