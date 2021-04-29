---
title: Начало работы — создание расширения обмена сообщениями
author: girliemac
description: Быстро создайте расширение обмена сообщениями Microsoft Teams с помощью набор средств.
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: 91a5a15697163ee9103607511047a6411a5acf1a
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068761"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="dde38-103">Создайте первое расширение обмена сообщениями для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dde38-103">Build your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="dde38-104">Существует два типа расширений обмена *сообщениями* Teams: [команды поиска](../messaging-extensions/how-to/search-commands/define-search-command.md) и [команды действий.](../messaging-extensions/how-to/action-commands/define-action-command.md)</span><span class="sxs-lookup"><span data-stu-id="dde38-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="dde38-105">В этом руководстве рассказывается о создании команды поиска *(также* известной как расширение обмена сообщениями на основе *поиска),* которая является ярлыком для поиска внешнего контента и совместного использования его в Teams.</span><span class="sxs-lookup"><span data-stu-id="dde38-105">This tutorial teaches you to create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="dde38-106">Пользователи могут получать доступ к командам поиска из командного или командного окна Teams.</span><span class="sxs-lookup"><span data-stu-id="dde38-106">Users can access search commands from the Teams compose or command box.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="dde38-107">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="dde38-107">What you'll learn</span></span>

* <span data-ttu-id="dde38-108">Создайте бот проекта приложения и расширение обмена сообщениями с помощью microsoft Teams набор средств для Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="dde38-108">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="dde38-109">Поймите конфигурации приложений и леса, соответствующие расширениям обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="dde38-109">Understand the app configurations and the scaffolding relevant to messaging extensions.</span></span>
* <span data-ttu-id="dde38-110">Локальное хост-приложение.</span><span class="sxs-lookup"><span data-stu-id="dde38-110">Host an app locally.</span></span>
* <span data-ttu-id="dde38-111">Настройка бота для расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="dde38-111">Configure the bot for your messaging extension.</span></span>
* <span data-ttu-id="dde38-112">Загрузка и тестирование расширения обмена сообщениями в Teams.</span><span class="sxs-lookup"><span data-stu-id="dde38-112">Sideload and test a messaging extension in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dde38-113">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="dde38-113">Prerequisites</span></span>

<span data-ttu-id="dde38-114">Убедитесь, что вы понимаете, как настроить и создать простое приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="dde38-114">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="dde38-115">Дополнительные сведения см. в [вашем первом приложении Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="dde38-115">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="dde38-116">1. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="dde38-116">1. Create your app project</span></span>

<span data-ttu-id="dde38-117">Программа Microsoft Teams набор средств позволяет настроить следующие компоненты для расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="dde38-117">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="dde38-118">**Конфигурации приложений и леса,** соответствующие расширениям обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="dde38-118">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="dde38-119">**Бот** для расширения обмена сообщениями, который автоматически зарегистрирован в службе Microsoft Azure Bot</span><span class="sxs-lookup"><span data-stu-id="dde38-119">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

<span data-ttu-id="dde38-120">**Создание проекта приложения**</span><span class="sxs-lookup"><span data-stu-id="dde38-120">**To create your app project**</span></span>

1. В Visual Studio коде выберите **Microsoft Teams** в левой панели действий и создайте новое приложение :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams.**
1. <span data-ttu-id="dde38-122">При запросе впишитесь в учетную запись разработки Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="dde38-122">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="dde38-123">На экране **Выберите проект** в **поиске** расширений обмена сообщениями  >  нажмите **кнопку JS (JavaScript).**</span><span class="sxs-lookup"><span data-stu-id="dde38-123">On the **Select project** screen, at **Messaging Extensions** > **Search**, click **JS (JavaScript)**.</span></span> 
1. <span data-ttu-id="dde38-124">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="dde38-124">Enter a name for your Teams app.</span></span> <span data-ttu-id="dde38-125">Это имя по умолчанию для вашего приложения, а также имя каталога проектов приложений на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="dde38-125">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="dde38-126">Выберите **Создать новый бот,** а затем нажмите **кнопку Создать регистрацию бота.**</span><span class="sxs-lookup"><span data-stu-id="dde38-126">Select **Create a new Bot** then click **Create Bot Registration** button.</span></span> <span data-ttu-id="dde38-127">В случае успешной работы новый бот будет иметь *зарегистрированный* статус.</span><span class="sxs-lookup"><span data-stu-id="dde38-127">If successful, your new bot will have a *Registered* status.</span></span> <span data-ttu-id="dde38-128">Теперь бот автоматически регистрируется в службе Microsoft Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="dde38-128">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 
1. <span data-ttu-id="dde38-129">Выберите **Готово** в нижней части экрана, чтобы настроить проект и сохранить проект на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="dde38-129">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="dde38-130">2. Понимание компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="dde38-130">2. Understand your app project components</span></span>

<span data-ttu-id="dde38-131">Большая часть конфигураций приложений и строительных лесов создается автоматически при создании проекта с командной набор средств.</span><span class="sxs-lookup"><span data-stu-id="dde38-131">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

* <span data-ttu-id="dde38-132">Конфигурации приложений. Чтобы просмотреть или обновить конфигурации расширения обмена сообщениями, выберите **App Studio** в наборе инструментов и перейдите к **расширениям обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="dde38-132">App configurations: To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>
* <span data-ttu-id="dde38-133">Строительные леса приложений. Строительные леса приложений предоставляют файл, расположенный в корневом каталоге проекта, для обработки того, как расширение обмена сообщениями (или технически, бот расширения обмена сообщениями) отвечает на поисковые запросы `botActivityHandler.js` в Teams. [](#4-configure-the-bot-for-your-messaging-extension)</span><span class="sxs-lookup"><span data-stu-id="dde38-133">App scaffolding: The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="dde38-134">3. Настройка безопасного туннеля в приложении</span><span class="sxs-lookup"><span data-stu-id="dde38-134">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="dde38-135">В целях тестирования разберем расширение обмена сообщениями на локальном веб-сервере (порт 3978).</span><span class="sxs-lookup"><span data-stu-id="dde38-135">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span> <span data-ttu-id="dde38-136">Вы собираетесь использовать [ngrok,](https://ngrok.com/download) чтобы настроить безопасный туннель для localhost.</span><span class="sxs-lookup"><span data-stu-id="dde38-136">You are going to use [ngrok](https://ngrok.com/download) to set up a secure tunnel to localhost.</span></span> <span data-ttu-id="dde38-137">Подробные [сведения см. в материале сборка первого бота для Microsoft Teams.](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet)</span><span class="sxs-lookup"><span data-stu-id="dde38-137">See [build your first bot for Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) for details.</span></span> 

1. <span data-ttu-id="dde38-138">Если вы еще не сделали этого, установите [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="dde38-138">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="dde38-139">В терминале запустите `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="dde38-139">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="dde38-140">Скопируйте URL-адрес HTTPS в выходе (например, ), так как `https://468b9ab725e9.ngrok.io` Teams требует подключений HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dde38-140">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

   <span data-ttu-id="dde38-141">С помощью этого URL-адреса Teams (для которой требуются подключения HTTPS) смогут пройдите туннель туда, где размещено ваше приложение (в `localhost` порту 3978).</span><span class="sxs-lookup"><span data-stu-id="dde38-141">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="dde38-142">4. Настройка бота для расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="dde38-142">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="dde38-143">Расширения обмена сообщениями используют боты для отправки и обработки запросов пользователей из Teams в вашу службу.</span><span class="sxs-lookup"><span data-stu-id="dde38-143">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="dde38-144">Бот должен быть зарегистрирован в службе Azure Bot Service, что было сделано при настройках приложения с помощью teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="dde38-144">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="dde38-145">Для получения и обработки поисковых запросов в расширении обмена сообщениями необходимо указать URL-адрес конечной точки бота.</span><span class="sxs-lookup"><span data-stu-id="dde38-145">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="dde38-146">Как правило, URL-адрес выглядит `https://HOST_URL/api/messages` как .</span><span class="sxs-lookup"><span data-stu-id="dde38-146">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="dde38-147">Это можно быстро настроить в наборе инструментов.</span><span class="sxs-lookup"><span data-stu-id="dde38-147">You can configure this quickly in the toolkit.</span></span>

1. В Visual Studio коде выберите **Microsoft Teams** в левой панели действий и выберите Open Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **набор средств**.
1. <span data-ttu-id="dde38-149">Перейдите **к ботам > существующие регистрации** ботов и выберите бот, созданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="dde38-149">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="dde38-150">В поле **адресов конечной точки** бота введите URL-адрес ngrok (например, ), где вы размещены бот и `https://468b9ab725e9.ngrok.io` приложение к `/api/messages` ней.</span><span class="sxs-lookup"><span data-stu-id="dde38-150">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

   <span data-ttu-id="dde38-151">Ваш бот сможет обрабатывать запросы в расширении обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="dde38-151">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="dde38-152">5. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="dde38-152">5. Build and run your app</span></span>

<span data-ttu-id="dde38-153">Вы настроили URL-адрес для расширения обмена сообщениями и настроили его для обработки поиска.</span><span class="sxs-lookup"><span data-stu-id="dde38-153">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="dde38-154">Пришло время, чтобы ваше приложение было запущено.</span><span class="sxs-lookup"><span data-stu-id="dde38-154">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="dde38-155">Откройте терминал и перейдите в корневой каталог проекта приложения</span><span class="sxs-lookup"><span data-stu-id="dde38-155">Open terminal and go to the root directory of your app project</span></span>
1. <span data-ttu-id="dde38-156">Запуск `npm install` .</span><span class="sxs-lookup"><span data-stu-id="dde38-156">Run `npm install`.</span></span>
1. <span data-ttu-id="dde38-157">Запуск `npm start` .</span><span class="sxs-lookup"><span data-stu-id="dde38-157">Run `npm start`.</span></span>

   <span data-ttu-id="dde38-158">В случае успеха вы увидите следующее сообщение, указывающее, что служба расширения обмена сообщениями прослушивает действия в `localhost` вашем :</span><span class="sxs-lookup"><span data-stu-id="dde38-158">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="dde38-159">6. Sideload your messaging extension in Teams</span><span class="sxs-lookup"><span data-stu-id="dde38-159">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="dde38-160">При запуске расширения обмена сообщениями его можно установить в Teams.</span><span class="sxs-lookup"><span data-stu-id="dde38-160">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="dde38-161">Если вы еще не перегружали приложение Teams до и не могли решить проблемы, следуйте [этим инструкциям.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="dde38-161">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="dde38-162">В Visual Studio коде выберите **клавишу F5** для запуска веб-клиента Teams.</span><span class="sxs-lookup"><span data-stu-id="dde38-162">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="dde38-163">В диалоговом окте установке приложения выберите **Добавить для меня**.</span><span class="sxs-lookup"><span data-stu-id="dde38-163">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="dde38-164">7. Проверьте расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="dde38-164">7. Test your messaging extension</span></span>

<span data-ttu-id="dde38-165">Узнайте, как работают расширения обмена сообщениями в чате Teams.</span><span class="sxs-lookup"><span data-stu-id="dde38-165">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="dde38-166">Запустите новый чат.</span><span class="sxs-lookup"><span data-stu-id="dde38-166">Start a new chat.</span></span> В поле составить выберите **Больше** и выберите приложение расширения обмена сообщениями, которое :::image type="icon" source="../assets/icons/teams-client-more.png"::: только что загружено.
1. <span data-ttu-id="dde38-168">Попробуйте найти что-то (например, **Билеты).**</span><span class="sxs-lookup"><span data-stu-id="dde38-168">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="dde38-169">Если приложение работает, вы увидите пример результатов поиска (вы можете добавить свои собственные позже).</span><span class="sxs-lookup"><span data-stu-id="dde38-169">If your app is working, you'll see sample search results (you can add your own later).</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Снимок экрана, показывающий, как в поле &quot;Команды&quot; используется расширение обмена сообщениями на основе поиска.":::

## <a name="troubleshooting"></a><span data-ttu-id="dde38-171">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="dde38-171">Troubleshooting</span></span>

<span data-ttu-id="dde38-172">Следующие сведения могут помочь, если у вас были проблемы с завершением этого руководства.</span><span class="sxs-lookup"><span data-stu-id="dde38-172">The following information may help if you had issues completing this tutorial.</span></span>

<span data-ttu-id="dde38-173">**Бот не подключен к Teams**</span><span class="sxs-lookup"><span data-stu-id="dde38-173">**Bot isn't connected to Teams**</span></span>

<span data-ttu-id="dde38-174">Если приложение установлено, но оно не работает, убедитесь, что бот расширения обмена сообщениями подключен к каналу [Teams службы ](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="dde38-174">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="dde38-175">Важно понимать, что это не то же самое, что канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="dde38-175">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="dde38-176">В этом случае канал — это способ подключения службы Azure Bot к Teams или другому поддерживаемом приложению майкрософт или сторонних [коммуникаций.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="dde38-176">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="dde38-177">См. также</span><span class="sxs-lookup"><span data-stu-id="dde38-177">See also</span></span>

* [<span data-ttu-id="dde38-178">Командная композиция или командная шкатулка</span><span class="sxs-lookup"><span data-stu-id="dde38-178">Teams compose or command box</span></span>](../messaging-extensions/what-are-messaging-extensions.md) 
* [<span data-ttu-id="dde38-179">Включить функцию разгрузки ссылок</span><span class="sxs-lookup"><span data-stu-id="dde38-179">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="dde38-180">Рекомендации по дизайну</span><span class="sxs-lookup"><span data-stu-id="dde38-180">Design guidelines</span></span>](../messaging-extensions/design/messaging-extension-design.md) 
* [<span data-ttu-id="dde38-181">Шаблоны пользовательского интерфейса, готовые к производству</span><span class="sxs-lookup"><span data-stu-id="dde38-181">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="dde38-182">Добавление проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="dde38-182">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="dde38-183">Создание расширения обмена сообщениями на основе действий</span><span class="sxs-lookup"><span data-stu-id="dde38-183">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="dde38-184">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="dde38-184">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)

## <a name="next-steps"></a><span data-ttu-id="dde38-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dde38-185">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dde38-186">Определить команды поиска</span><span class="sxs-lookup"><span data-stu-id="dde38-186">Define search commands</span></span>](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="dde38-187">Реагирование на поиск пользователей</span><span class="sxs-lookup"><span data-stu-id="dde38-187">Respond to users' searches</span></span>](../messaging-extensions/how-to/search-commands/respond-to-search.md)