---
title: Начало работы — создание расширения обмена сообщениями
author: heath-hamilton
description: Быстро Создайте расширение системы обмена сообщениями Microsoft Teams с помощью набора инструментов Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 160878d92969d57680e6fa25eb6fc13e82bf2a82
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931752"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="dbf3d-103">Создание расширения обмена сообщениями для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dbf3d-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="dbf3d-104">Существует два типа *расширений для обмена сообщениями* в teams: [команды поиска](../messaging-extensions/how-to/search-commands/define-search-command.md) и [команды действий](../messaging-extensions/how-to/action-commands/define-action-command.md).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-104">There are two types of Teams app *messaging extensions* : [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="dbf3d-105">На этом занятии вы создадите *команду поиска* (также называемую *расширением обмена сообщениями на основе поиска* ), которая является ярлыком для поиска внешнего контента и предоставления общего доступа к ним в Teams.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension* ), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="dbf3d-106">Пользователи могут получить доступ к командам поиска из [поля "Создание команд" или "команда"](../messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="dbf3d-107">Ваше назначение</span><span class="sxs-lookup"><span data-stu-id="dbf3d-107">Your assignment</span></span>

<span data-ttu-id="dbf3d-108">Служба технической поддержки организации взаимодействуют с пользователями в Teams, но эти билеты размещаются в отдельной системе.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="dbf3d-109">Это означает, что сотрудники службы поддержки должны постоянно переходить между приложениями и перемещаться между ними.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="dbf3d-110">Вы узнаете, как можно уменьшить это большое количество контекстных переключений, создав простой модуль обмена сообщениями на основе поиска для Teams.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="dbf3d-111">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="dbf3d-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="dbf3d-112">Создание проекта приложения и расширения обмена сообщениями Bot с помощью набора инструментов Microsoft Teams для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="dbf3d-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="dbf3d-113">Определите конфигурации приложений и некоторые шаблоны формирования шаблонов, относящиеся к расширениям обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-113">Identify the app configurations and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="dbf3d-114">Локальное размещение приложения</span><span class="sxs-lookup"><span data-stu-id="dbf3d-114">Host an app locally</span></span>
> * <span data-ttu-id="dbf3d-115">Настройка почтового робота для расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="dbf3d-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="dbf3d-116">Загрузка неопубликованных и тестирование расширения обмена сообщениями в Teams</span><span class="sxs-lookup"><span data-stu-id="dbf3d-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dbf3d-117">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="dbf3d-117">Before you begin</span></span>

<span data-ttu-id="dbf3d-118">Если вы еще не сделали это, убедитесь, что вы [знаете и установите необходимые компоненты для разработки Teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="dbf3d-119">1. Создайте проект приложения.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-119">1. Create your app project</span></span>

<span data-ttu-id="dbf3d-120">Набор средств Microsoft Teams позволяет настроить следующие компоненты для расширения системы обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="dbf3d-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="dbf3d-121">**Конфигурации приложений и формирование шаблонов,** относящиеся к расширениям обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="dbf3d-121">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="dbf3d-122">**Bot** для расширения обмена сообщениями, автоматически регистрируемого в службе Microsoft Azure Bot</span><span class="sxs-lookup"><span data-stu-id="dbf3d-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="dbf3d-123">Если вы еще не создали проект приложения Teams, возможно, вам будет полезно выполнить приведенные [выше инструкции по](../build-your-first-app/build-and-run.md) более подробному объяснению проектов.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
1. <span data-ttu-id="dbf3d-125">При появлении соответствующего запроса войдите в систему с помощью учетной записи разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-125">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="dbf3d-126">На экране **добавить возможности** выберите **расширение системы обмена сообщениями** , а затем нажмите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-126">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="dbf3d-127">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-127">Enter a name for your Teams app.</span></span> <span data-ttu-id="dbf3d-128">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="dbf3d-128">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="dbf3d-129">На экране **Настройка расширения обмена сообщениями** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="dbf3d-129">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="dbf3d-130">Выберите вариант только **на основе поиска** для типа расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-130">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="dbf3d-131">Выберите **создать новый Bot,** а затем **создайте регистрацию для ленты**.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-131">Select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="dbf3d-132">В случае успеха новый робот будет иметь **зарегистрированное** состояние.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-132">If successful, your new bot will have a **Registered** status.</span></span>
    1. <span data-ttu-id="dbf3d-133">Пока нажмите кнопку **нет** для параметра link унфурлинг.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-133">For now, select **No** for the link unfurling option.</span></span>
1. <span data-ttu-id="dbf3d-134">В нижней части экрана нажмите кнопку **Готово** , чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="dbf3d-135">2. определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="dbf3d-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="dbf3d-136">Многие конфигурации приложений и формирование шаблонов настраиваются автоматически при создании проекта с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-136">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="dbf3d-137">Конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="dbf3d-137">App configurations</span></span>

<span data-ttu-id="dbf3d-138">Чтобы просмотреть или изменить конфигурации расширения системы обмена сообщениями, выберите **app Studio** в наборе инструментов и перейдите к разделу **расширения обмена сообщениями**.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-138">To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="dbf3d-139">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="dbf3d-139">App scaffolding</span></span>

<span data-ttu-id="dbf3d-140">Формирование шаблонов приложений предоставляет `botActivityHandler.js` файл, расположенный в корневом каталоге проекта, для обработки того, как расширение системы обмена сообщениями (или техническим процессом [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) реагирует на поисковые запросы в Teams.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="dbf3d-141">3. Настройка безопасного туннеля для приложения</span><span class="sxs-lookup"><span data-stu-id="dbf3d-141">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="dbf3d-142">В целях тестирования давайте разместите расширение обмена сообщениями на локальном веб-сервере (порт 3978).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-142">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="dbf3d-143">Если вы еще не сделали это, установите [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-143">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="dbf3d-144">В терминале запустите `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="dbf3d-144">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="dbf3d-145">Скопируйте URL-адрес HTTPS в выходных данных (например, `https://468b9ab725e9.ngrok.io` ), так как для Teams необходимы HTTPS-подключения.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-145">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="dbf3d-146">При использовании этого URL-адреса Teams (для которых требуются HTTPS-подключения) смогут подключаться к месту размещения приложения ( `localhost` на порте 3978).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-146">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="dbf3d-147">4. Настройка Bot для расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="dbf3d-147">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="dbf3d-148">Расширения обмена сообщениями основываются на боты для отправки и обработки запросов пользователей из Teams в размещенную службу.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-148">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="dbf3d-149">Робот должен быть зарегистрирован в службе Azure Bot, которая была выполнена при настройке приложения с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-149">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="dbf3d-150">По-прежнему необходимо указать URL-адрес конечной точки Bot для получения и обработки поисковых запросов в вашем расширении системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-150">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="dbf3d-151">Как правило, URL-адрес выглядит так `https://HOST_URL/api/messages` :</span><span class="sxs-lookup"><span data-stu-id="dbf3d-151">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="dbf3d-152">Вы можете быстро настроить его в наборе инструментов.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-152">You can configure this quickly in the toolkit.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели действий, а затем выберите пункт **Открыть набор средств Microsoft Teams**.
1. <span data-ttu-id="dbf3d-154">Перейдите в **боты > существующие регистрации Bot** и выберите робот, созданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-154">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="dbf3d-155">В поле **адрес конечной точки Bot** введите URL-адрес ngrok (например,), на `https://468b9ab725e9.ngrok.io` котором размещается Bot и добавьте `/api/messages` к нему.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-155">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

<span data-ttu-id="dbf3d-156">Ваш робот сможет обрабатывать запросы в вашем расширении системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-156">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="dbf3d-157">5. Построение и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="dbf3d-157">5. Build and run your app</span></span>

<span data-ttu-id="dbf3d-158">Вы настроили URL-адрес для размещения своего расширения обмена сообщениями и настройки его для обработки запросов поиска.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-158">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="dbf3d-159">Самое время заставить ваше приложение работать и работать.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="dbf3d-160">В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .</span><span class="sxs-lookup"><span data-stu-id="dbf3d-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="dbf3d-161">Выполните команду `npm start` .</span><span class="sxs-lookup"><span data-stu-id="dbf3d-161">Run `npm start`.</span></span>

<span data-ttu-id="dbf3d-162">В случае успеха появится следующее сообщение о том, что служба расширения обмена сообщениями прослушивает действия в `localhost` :</span><span class="sxs-lookup"><span data-stu-id="dbf3d-162">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="dbf3d-163">6. Загрузка неопубликованных своего расширения обмена сообщениями в Teams</span><span class="sxs-lookup"><span data-stu-id="dbf3d-163">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="dbf3d-164">Если ваш модуль обмена сообщениями работает, вы можете установить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-164">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="dbf3d-165">Если вы еще не неопубликованные приложение Teams до и не выпустили проблемы, выполните указанные ниже [действия](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="dbf3d-166">В Visual Studio Code нажмите клавишу **F5** , чтобы запустить веб-клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="dbf3d-167">В диалоговом окне Установка приложения нажмите кнопку " **Добавить** ".</span><span class="sxs-lookup"><span data-stu-id="dbf3d-167">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="dbf3d-168">7. Тестирование расширения системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="dbf3d-168">7. Test your messaging extension</span></span>

<span data-ttu-id="dbf3d-169">Узнайте, как работают расширения обмена сообщениями в чате Teams.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-169">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="dbf3d-170">Начните новый сеанс разговора.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-170">Start a new chat.</span></span> В поле Создание нажмите кнопку **Дополнительно** :::image type="icon" source="../assets/icons/teams-client-more.png"::: и выберите приложение расширения обмена сообщениями, которое вы только что неопубликованные.
1. <span data-ttu-id="dbf3d-172">Попробуйте выполнить поиск чего-либо (например, **билетов** ).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-172">Try searching for something (for example, **Tickets** ).</span></span> <span data-ttu-id="dbf3d-173">Если ваше приложение работает, вы увидите пример результатов поиска (вы можете добавить его позже).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-173">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Снимок экрана, демонстрирующий использование расширения обмена сообщениями на основе поиска в поле _OL_QUOTE_PLACEHOLDER_Создание Teams_OL_QUOTE_PLACEHOLDER_.":::

## <a name="well-done"></a><span data-ttu-id="dbf3d-175">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="dbf3d-175">Well done</span></span>

<span data-ttu-id="dbf3d-176">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="dbf3d-176">Congratulations!</span></span> <span data-ttu-id="dbf3d-177">У вас есть основные расширения системы обмена сообщениями Teams, которые задают поиск внешнего контента в поле "создать" или "команда".</span><span class="sxs-lookup"><span data-stu-id="dbf3d-177">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbf3d-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dbf3d-178">Next steps</span></span>

<span data-ttu-id="dbf3d-179">Чтобы продолжить и создать полнофункциональное расширение системы обмена сообщениями, ознакомьтесь со следующими страницами:</span><span class="sxs-lookup"><span data-stu-id="dbf3d-179">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="dbf3d-180">[Определите команды поиска](../messaging-extensions/how-to/search-commands/define-search-command.md) , связанные со службой.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-180">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="dbf3d-181">Настройте службу для [реагирования на поиск пользователей](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-181">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dbf3d-182">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="dbf3d-182">Troubleshooting</span></span>

<span data-ttu-id="dbf3d-183">Приведенные ниже сведения помогут вам устранить проблемы, связанные с выполнением этого руководства.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-183">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="dbf3d-184">Bot не подключены к Teams</span><span class="sxs-lookup"><span data-stu-id="dbf3d-184">Bot isn't connected to Teams</span></span>

<span data-ttu-id="dbf3d-185">Если вы установили приложение, но оно не работает, убедитесь, что линия канала для расширения обмена сообщениями [подключена к *каналу* команд службы Azure Bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-185">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="dbf3d-186">Важно понимать, что это не то же самое, что и канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="dbf3d-186">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="dbf3d-187">В этом случае каналом является способ подключения службы Azure Bot к Teams или другому [поддерживаемому Microsoft или стороннему приложению для общения](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="dbf3d-187">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="dbf3d-188">Подробнее</span><span class="sxs-lookup"><span data-stu-id="dbf3d-188">Learn more</span></span>

* [<span data-ttu-id="dbf3d-189">Включение функции Link унфурлинг</span><span class="sxs-lookup"><span data-stu-id="dbf3d-189">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="dbf3d-190">Добавить аутентификацию</span><span class="sxs-lookup"><span data-stu-id="dbf3d-190">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="dbf3d-191">Создание расширения обмена сообщениями на основе действий</span><span class="sxs-lookup"><span data-stu-id="dbf3d-191">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="dbf3d-192">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="dbf3d-192">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
