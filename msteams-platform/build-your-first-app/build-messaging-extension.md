---
title: Начать работу - Создайте расширение обмена сообщениями
author: girliemac
description: Быстро создайте Microsoft Teams обмена сообщениями с помощью Microsoft Teams набор средств.
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: c120a5b5d878c549cde008c3e1ccc71743a4e24f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566063"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="c1d47-103">Создайте свое первое расширение обмена сообщениями для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c1d47-103">Build your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="c1d47-104">Существует два типа Teams *обмена сообщениями: команды* поиска [и](../messaging-extensions/how-to/search-commands/define-search-command.md) [команды действий.](../messaging-extensions/how-to/action-commands/define-action-command.md)</span><span class="sxs-lookup"><span data-stu-id="c1d47-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="c1d47-105">Этот учебник научит вас создавать команду поиска *(также известную* как расширение обмена сообщениями на *основе поиска),* которая является ярлыком для поиска внешнего контента и обмена им в Teams.</span><span class="sxs-lookup"><span data-stu-id="c1d47-105">This tutorial teaches you to create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="c1d47-106">Пользователи могут получить доступ к командам поиска из Teams составить или командовать окном.</span><span class="sxs-lookup"><span data-stu-id="c1d47-106">Users can access search commands from the Teams compose or command box.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="c1d47-107">Чему вы научитесь</span><span class="sxs-lookup"><span data-stu-id="c1d47-107">What you'll learn</span></span>

* <span data-ttu-id="c1d47-108">Создайте проект приложения и бот расширения обмена сообщениями, используя Microsoft Teams набор средств для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c1d47-108">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="c1d47-109">Поймите конфигурации приложений и леса, имеющие отношение к расширениям обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c1d47-109">Understand the app configurations and the scaffolding relevant to messaging extensions.</span></span>
* <span data-ttu-id="c1d47-110">Хост приложения локально.</span><span class="sxs-lookup"><span data-stu-id="c1d47-110">Host an app locally.</span></span>
* <span data-ttu-id="c1d47-111">Настройте бота для расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c1d47-111">Configure the bot for your messaging extension.</span></span>
* <span data-ttu-id="c1d47-112">Sideload и протестировать расширение обмена сообщениями в Teams.</span><span class="sxs-lookup"><span data-stu-id="c1d47-112">Sideload and test a messaging extension in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1d47-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c1d47-113">Prerequisites</span></span>

<span data-ttu-id="c1d47-114">Убедитесь, что вы понимаете, как настроить и построить простой Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="c1d47-114">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="c1d47-115">Для получения дополнительной [информации, см Microsoft Teams.](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="c1d47-115">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="c1d47-116">1. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="c1d47-116">1. Create your app project</span></span>

<span data-ttu-id="c1d47-117">Система Microsoft Teams набор средств позволяет настроить следующие компоненты для расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="c1d47-117">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="c1d47-118">**Конфигурации приложений и леса, имеющие** отношение к расширениям обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c1d47-118">**App configurations and scaffolding** relevant to messaging extensions.</span></span>
* <span data-ttu-id="c1d47-119">**Бот** для расширения обмена сообщениями, который автоматически регистрируется в Microsoft Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="c1d47-119">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="c1d47-120">**Создание проекта приложения**</span><span class="sxs-lookup"><span data-stu-id="c1d47-120">**To create your app project**</span></span>

1. В Visual Studio Code выберите **Microsoft Teams левой** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: стороне активности и **выберите Создать новое Teams приложение.**
1. <span data-ttu-id="c1d47-122">По запросу вопишитесь на свой аккаунт Microsoft 365 разработки.</span><span class="sxs-lookup"><span data-stu-id="c1d47-122">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="c1d47-123">На **экране проекта Select,** в **поиске расширений**  >  **сообщений нажмите** **JS (JavaScript).**</span><span class="sxs-lookup"><span data-stu-id="c1d47-123">On the **Select project** screen, at **Messaging Extensions** > **Search**, click **JS (JavaScript)**.</span></span> 
1. <span data-ttu-id="c1d47-124">Введите имя для вашего Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="c1d47-124">Enter a name for your Teams app.</span></span> <span data-ttu-id="c1d47-125">Это имя по умолчанию для вашего приложения, а также название каталога проекта приложения на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="c1d47-125">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="c1d47-126">Выберите **Создать новый Бот затем нажмите** **Создать Bot Регистрация кнопку.**</span><span class="sxs-lookup"><span data-stu-id="c1d47-126">Select **Create a new Bot** then click **Create Bot Registration** button.</span></span> <span data-ttu-id="c1d47-127">В случае успеха, ваш новый бот будет иметь статус *Зарегистрированный.*</span><span class="sxs-lookup"><span data-stu-id="c1d47-127">If successful, your new bot will have a *Registered* status.</span></span> <span data-ttu-id="c1d47-128">Теперь ваш бот автоматически регистрируется в Microsoft Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="c1d47-128">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 
1. <span data-ttu-id="c1d47-129">**Выберите** отделку в нижней части экрана, чтобы настроить проект и сохранить проект на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="c1d47-129">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="c1d47-130">2. Понимание компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="c1d47-130">2. Understand your app project components</span></span>

<span data-ttu-id="c1d47-131">Большая часть конфигураций приложений и строительных лесов настроены автоматически при создании проекта с помощью Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="c1d47-131">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

* <span data-ttu-id="c1d47-132">Конфигурации приложений: Для просмотра или обновления конфигураций расширения обмена сообщениями выберите **App Studio в** наборе инструментов и перейдите к **расширениям обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="c1d47-132">App configurations: To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>
* <span data-ttu-id="c1d47-133">Строительные леса приложения: строительные леса приложения предоставляют `botActivityHandler.js` файл, расположенный в корневом каталоге вашего проекта, для обработки того, как расширение обмена сообщениями (или технически, [бот расширения обмена сообщениями)](#4-configure-the-bot-for-your-messaging-extension)реагирует на поисковые запросы в Teams.</span><span class="sxs-lookup"><span data-stu-id="c1d47-133">App scaffolding: The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="c1d47-134">3. Настройка безопасного туннеля для приложения</span><span class="sxs-lookup"><span data-stu-id="c1d47-134">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="c1d47-135">Для целей тестирования давайте разохозим расширение обмена сообщениями на локальном веб-сервере (порт 3978).</span><span class="sxs-lookup"><span data-stu-id="c1d47-135">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span> <span data-ttu-id="c1d47-136">Вы собираетесь использовать [ngrok для](https://ngrok.com/download) настройки безопасного туннеля для localhost.</span><span class="sxs-lookup"><span data-stu-id="c1d47-136">You are going to use [ngrok](https://ngrok.com/download) to set up a secure tunnel to localhost.</span></span> <span data-ttu-id="c1d47-137">Для [получения подробной информации можно Microsoft Teams первый](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) бот для получения подробной информации.</span><span class="sxs-lookup"><span data-stu-id="c1d47-137">See [build your first bot for Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) for details.</span></span> 

1. <span data-ttu-id="c1d47-138">Если вы еще не сделали этого, [установите ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="c1d47-138">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="c1d47-139">В терминале, запустить `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="c1d47-139">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="c1d47-140">Копирование URL-адреса HTTPS в выходе (например, `https://468b9ab725e9.ngrok.io` ) с тех пор, как Teams требует подключения HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c1d47-140">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

   <span data-ttu-id="c1d47-141">С помощью этого URL Teams (который требует подключения HTTPS) сможет туннель, где вы хостинг вашего приложения `localhost` (на порт 3978).</span><span class="sxs-lookup"><span data-stu-id="c1d47-141">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="c1d47-142">4. Настройте бота для расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c1d47-142">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="c1d47-143">Расширения обмена сообщениями полагаются на ботов для отправки и обработки запросов пользователей Teams в ваш хостинг-сервис.</span><span class="sxs-lookup"><span data-stu-id="c1d47-143">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="c1d47-144">Бот должен быть зарегистрирован в службе Azure Bot, что было сделано при настройке приложения с помощью Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="c1d47-144">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="c1d47-145">Вы все еще должны указать URL-адрес конечной точки бота для получения и обработки поисковых запросов в расширении обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c1d47-145">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="c1d47-146">Как правило, URL выглядит `https://HOST_URL/api/messages` как .</span><span class="sxs-lookup"><span data-stu-id="c1d47-146">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="c1d47-147">Вы можете настроить это быстро в наборе инструментов.</span><span class="sxs-lookup"><span data-stu-id="c1d47-147">You can configure this quickly in the toolkit.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams левой** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: стойке активности и выберите Open **Microsoft Teams набор средств.**
1. <span data-ttu-id="c1d47-149">Перейти к **Bots > существующих регистраций ботов и** выбрать бота вы создали во время установки.</span><span class="sxs-lookup"><span data-stu-id="c1d47-149">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="c1d47-150">В поле **адреса конечной точки** Bot введите URL ngrok (например, `https://468b9ab725e9.ngrok.io` ), где вы принимаете бота и придаток `/api/messages` к нему.</span><span class="sxs-lookup"><span data-stu-id="c1d47-150">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

   <span data-ttu-id="c1d47-151">Ваш бот сможет обрабатывать запросы в вашем расширении обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c1d47-151">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="c1d47-152">5. Создание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="c1d47-152">5. Build and run your app</span></span>

<span data-ttu-id="c1d47-153">Вы настроили URL-адрес для размещения расширения обмена сообщениями и настроили его для обработки поиска.</span><span class="sxs-lookup"><span data-stu-id="c1d47-153">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="c1d47-154">Пришло время, чтобы получить ваше приложение и работает.</span><span class="sxs-lookup"><span data-stu-id="c1d47-154">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="c1d47-155">Откройте терминал и перейдите в корневой каталог проекта приложения.</span><span class="sxs-lookup"><span data-stu-id="c1d47-155">Open terminal and go to the root directory of your app project.</span></span>
1. <span data-ttu-id="c1d47-156">Запуск `npm install` .</span><span class="sxs-lookup"><span data-stu-id="c1d47-156">Run `npm install`.</span></span>
1. <span data-ttu-id="c1d47-157">Запуск `npm start` .</span><span class="sxs-lookup"><span data-stu-id="c1d47-157">Run `npm start`.</span></span>

   <span data-ttu-id="c1d47-158">В случае успеха вы видите следующее сообщение, указывающее на то, что служба расширения обмена сообщениями прослушивает действия в вашей `localhost` службе:</span><span class="sxs-lookup"><span data-stu-id="c1d47-158">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="c1d47-159">6. Sideload расширение обмена сообщениями в Teams</span><span class="sxs-lookup"><span data-stu-id="c1d47-159">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="c1d47-160">С запуском расширения обмена сообщениями вы можете установить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="c1d47-160">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="c1d47-161">Если вы еще не перегрузили приложение Teams и не затеяли проблемы, следуйте этим [инструкциям.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="c1d47-161">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="c1d47-162">В Visual Studio Code, выберите **F5** ключ для запуска Teams веб-клиента.</span><span class="sxs-lookup"><span data-stu-id="c1d47-162">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="c1d47-163">В диалоге установки приложения, **выберите Добавить для меня**.</span><span class="sxs-lookup"><span data-stu-id="c1d47-163">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="c1d47-164">7. Проверьте расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c1d47-164">7. Test your messaging extension</span></span>

<span data-ttu-id="c1d47-165">Узнайте, как расширения обмена сообщениями работают в Teams чате.</span><span class="sxs-lookup"><span data-stu-id="c1d47-165">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="c1d47-166">Запустите новый чат.</span><span class="sxs-lookup"><span data-stu-id="c1d47-166">Start a new chat.</span></span> В поле compose выберите **More и выберите** :::image type="icon" source="../assets/icons/teams-client-more.png"::: приложение для расширения обмена сообщениями, которое вы только что перезагрузили.
1. <span data-ttu-id="c1d47-168">Попробуйте найти что-то (например, **билеты).**</span><span class="sxs-lookup"><span data-stu-id="c1d47-168">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="c1d47-169">Если ваше приложение работает, вы увидите результаты поиска образцов (вы можете добавить свой собственный позже).</span><span class="sxs-lookup"><span data-stu-id="c1d47-169">If your app is working, you'll see sample search results (you can add your own later).</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Скриншот, показывающий, как в приложении используется расширение обмена сообщениями на основе поиска Teams составить поле.":::

## <a name="troubleshooting"></a><span data-ttu-id="c1d47-171">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="c1d47-171">Troubleshooting</span></span>

<span data-ttu-id="c1d47-172">Следующая информация может помочь, если у вас были проблемы с завершением этого учебника.</span><span class="sxs-lookup"><span data-stu-id="c1d47-172">The following information may help if you had issues completing this tutorial.</span></span>

<span data-ttu-id="c1d47-173">**Бот не подключен к Teams**</span><span class="sxs-lookup"><span data-stu-id="c1d47-173">**Bot isn't connected to Teams**</span></span>

<span data-ttu-id="c1d47-174">Если вы установили приложение, но оно не работает, убедитесь, что бот расширения обмена [сообщениями подключен к каналу службы Azure Bot *Teams.*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c1d47-174">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="c1d47-175">Важно понимать, что это не то же самое, что канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="c1d47-175">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="c1d47-176">В этом случае канал — это способ подключения службы Azure Bot к Teams или другому [поддерживаемому приложению microsoft или сторонних коммуникаций.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c1d47-176">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="c1d47-177">См. также</span><span class="sxs-lookup"><span data-stu-id="c1d47-177">See also</span></span>

* [<span data-ttu-id="c1d47-178">Teams сочинять или командовать окном</span><span class="sxs-lookup"><span data-stu-id="c1d47-178">Teams compose or command box</span></span>](../messaging-extensions/what-are-messaging-extensions.md) 
* [<span data-ttu-id="c1d47-179">Включите функцию разворачивания ссылок</span><span class="sxs-lookup"><span data-stu-id="c1d47-179">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="c1d47-180">Рекомендации по дизайну</span><span class="sxs-lookup"><span data-stu-id="c1d47-180">Design guidelines</span></span>](../messaging-extensions/design/messaging-extension-design.md) 
* [<span data-ttu-id="c1d47-181">Готовые к производству шаблоны пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="c1d47-181">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="c1d47-182">Добавление проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="c1d47-182">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="c1d47-183">Создание расширения обмена сообщениями на основе действий</span><span class="sxs-lookup"><span data-stu-id="c1d47-183">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="c1d47-184">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c1d47-184">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)

## <a name="next-steps"></a><span data-ttu-id="c1d47-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1d47-185">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c1d47-186">Определить команды поиска</span><span class="sxs-lookup"><span data-stu-id="c1d47-186">Define search commands</span></span>](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c1d47-187">Ответ на поиск пользователей</span><span class="sxs-lookup"><span data-stu-id="c1d47-187">Respond to users' searches</span></span>](../messaging-extensions/how-to/search-commands/respond-to-search.md)
