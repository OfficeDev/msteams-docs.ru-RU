---
title: Создание расширения для обмена сообщениями в Teams
author: heath-hamilton
description: Узнайте, как создать расширение для обмена сообщениями для первого приложения Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: 4fd35f6d5cc4b4ba202cb4276386918a5d88d692
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237820"
---
# <a name="build-a-teams-messaging-extension"></a><span data-ttu-id="21cf2-103">Создание расширения для обмена сообщениями в Teams</span><span class="sxs-lookup"><span data-stu-id="21cf2-103">Build a Teams messaging extension</span></span>

<span data-ttu-id="21cf2-104">Существует два типа *расширений для обмена сообщениями*в teams: [команды поиска](../messaging-extensions/how-to/search-commands/define-search-command.md) и [команды действий](../messaging-extensions/how-to/action-commands/define-action-command.md).</span><span class="sxs-lookup"><span data-stu-id="21cf2-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="21cf2-105">На этом занятии вы создадите *команду поиска* (также называемую *расширением обмена сообщениями на основе поиска*), которая является ярлыком для поиска внешнего контента и предоставления общего доступа к ним в Teams.</span><span class="sxs-lookup"><span data-stu-id="21cf2-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="21cf2-106">Пользователи могут получить доступ к командам поиска из [поля "Создание команд" или "команда"](../messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="21cf2-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="21cf2-107">Ваше назначение</span><span class="sxs-lookup"><span data-stu-id="21cf2-107">Your assignment</span></span>

<span data-ttu-id="21cf2-108">Служба технической поддержки организации взаимодействуют с пользователями в Teams, но эти билеты размещаются в отдельной системе.</span><span class="sxs-lookup"><span data-stu-id="21cf2-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="21cf2-109">Это означает, что сотрудники службы поддержки должны постоянно переходить между приложениями и перемещаться между ними.</span><span class="sxs-lookup"><span data-stu-id="21cf2-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="21cf2-110">Вы узнаете, как можно уменьшить это большое количество контекстных переключений, создав простой модуль обмена сообщениями на основе поиска для Teams.</span><span class="sxs-lookup"><span data-stu-id="21cf2-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="21cf2-111">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="21cf2-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="21cf2-112">Создание проекта приложения и расширения обмена сообщениями Bot с помощью набора инструментов Microsoft Teams для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="21cf2-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="21cf2-113">Определите свойства манифеста приложения и некоторые шаблоны формирования шаблонов, относящиеся к расширениям обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="21cf2-113">Identify the app manifest properties and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="21cf2-114">Локальное размещение приложения</span><span class="sxs-lookup"><span data-stu-id="21cf2-114">Host an app locally</span></span>
> * <span data-ttu-id="21cf2-115">Настройка почтового робота для расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="21cf2-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="21cf2-116">Загрузка неопубликованных и тестирование расширения обмена сообщениями в Teams</span><span class="sxs-lookup"><span data-stu-id="21cf2-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="21cf2-117">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="21cf2-117">Before you begin</span></span>

<span data-ttu-id="21cf2-118">Если вы еще не сделали это, убедитесь, что вы [знаете и установите необходимые компоненты для разработки Teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="21cf2-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="21cf2-119">1. Создайте проект приложения.</span><span class="sxs-lookup"><span data-stu-id="21cf2-119">1. Create your app project</span></span>

<span data-ttu-id="21cf2-120">Набор средств Microsoft Teams позволяет настроить следующие компоненты для расширения системы обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="21cf2-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="21cf2-121">**Манифест приложения и формирование шаблонов,** относящиеся к расширениям обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="21cf2-121">**App manifest and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="21cf2-122">**Bot** для расширения обмена сообщениями, автоматически регистрируемого в службе Microsoft Azure Bot</span><span class="sxs-lookup"><span data-stu-id="21cf2-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="21cf2-123">Если вы еще не создали проект приложения Teams, возможно, вам будет полезно выполнить приведенные [выше инструкции по](../build-your-first-app/build-and-run.md) более подробному объяснению проектов.</span><span class="sxs-lookup"><span data-stu-id="21cf2-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
1. <span data-ttu-id="21cf2-125">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="21cf2-125">Enter a name for your Teams app.</span></span> <span data-ttu-id="21cf2-126">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="21cf2-126">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="21cf2-127">На экране **добавить возможности** выберите **расширение системы обмена сообщениями** , а затем нажмите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="21cf2-127">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="21cf2-128">На экране **Настройка расширения обмена сообщениями** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="21cf2-128">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="21cf2-129">Выберите вариант только **на основе поиска** для типа расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="21cf2-129">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="21cf2-130">Выберите **создать новый робот** **и войдите в систему,** используя учетную запись Microsoft 365 для разработки.</span><span class="sxs-lookup"><span data-stu-id="21cf2-130">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span>
    1. <span data-ttu-id="21cf2-131">Сохраните идентификатор и пароль почтового робота (это необходимо сделать чуть позже).</span><span class="sxs-lookup"><span data-stu-id="21cf2-131">Store your bot ID and password (you need this a little later).</span></span>
    1. <span data-ttu-id="21cf2-132">Необязательно Введите настраиваемое имя для Bot и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="21cf2-132">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="21cf2-133">(Это не имя уже указанного приложения Teams.)</span><span class="sxs-lookup"><span data-stu-id="21cf2-133">(This is not the name of the Teams app you already specified.)</span></span>
    1. <span data-ttu-id="21cf2-134">Пока нажмите кнопку **нет** для параметра link унфурлинг.</span><span class="sxs-lookup"><span data-stu-id="21cf2-134">For now, select **No** for the link unfurling option.</span></span></br>
:::image type="content" source="../assets/images/build-your-first-app/choose-me-search.png" alt-text="Иллюстрация, на которой показано, как в наборе инструментов Teams войти в свою учетную запись Microsoft 365, чтобы создать новый почтовый робот для расширения обмена сообщениями.":::
1. <span data-ttu-id="21cf2-136">В нижней части экрана нажмите кнопку **Готово** , чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="21cf2-136">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="21cf2-137">2. определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="21cf2-137">2. Identify relevant app project components</span></span>

<span data-ttu-id="21cf2-138">Большинство манифестов и шаблонов приложений настраиваются автоматически при создании проекта с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="21cf2-138">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="21cf2-139">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="21cf2-139">App manifest</span></span>

<span data-ttu-id="21cf2-140">В следующем фрагменте кода из манифеста приложения ( `manifest.json` файл в каталоге проекта `.publish` ) показаны свойства и значения по умолчанию, относящиеся к расширениям обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="21cf2-140">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to messaging extensions.</span></span>

```JSON
"composeExtensions": [
    {
        "botId": "{botId0}",
        "canUpdateConfiguration": true,
        "commands": [
            {
                "id": "searchQuery",
                "context": [
                    "compose",
                    "commandBox"
                ],
                "description": "Test command to run query",
                "title": "Search",
                "type": "query",
                "parameters": [
                    {
                        "name": "searchQuery",
                        "title": "Search Query",
                        "description": "Your search query",
                        "inputType": "text"
                    }
                ]
            }
        ]
    }
],
```

<span data-ttu-id="21cf2-141">Давайте взглянем на некоторые из свойств, которые создает набор средств.</span><span class="sxs-lookup"><span data-stu-id="21cf2-141">Let's understand some of the properties the toolkit created for you.</span></span> <span data-ttu-id="21cf2-142">(Обратитесь к полному списку поддерживаемых [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) свойств.)</span><span class="sxs-lookup"><span data-stu-id="21cf2-142">(See the full list of supported [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) properties.)</span></span>

* <span data-ttu-id="21cf2-143">`botId`: Идентификатор созданного робота, созданного вами с помощью настройки проекта.</span><span class="sxs-lookup"><span data-stu-id="21cf2-143">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="21cf2-144">(Хранимая в `{botId0}` , вы можете найти фактический идентификатор в `Development.env` .)</span><span class="sxs-lookup"><span data-stu-id="21cf2-144">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="21cf2-145">`commands`: Доступные команды для расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="21cf2-145">`commands`: Available commands for the messaging extension.</span></span> <span data-ttu-id="21cf2-146">Набор средств, который обеспечивает формирование шаблонов для команды поиска.</span><span class="sxs-lookup"><span data-stu-id="21cf2-146">The toolkit provided you scaffolding for a search command.</span></span>
* <span data-ttu-id="21cf2-147">`context`: Где пользователи могут вызывать расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="21cf2-147">`context`: Where users can invoke the messaging extension.</span></span> <span data-ttu-id="21cf2-148">В этом случае вы можете запустить расширение системы обмена сообщениями из поля команда "создать" или "команда".</span><span class="sxs-lookup"><span data-stu-id="21cf2-148">In this case, you can launch the messaging extension from the Teams compose or command box.</span></span>
* <span data-ttu-id="21cf2-149">`description`: Текст справки по пользовательскому интерфейсу, указывающий, что делает команда или как ее использовать.</span><span class="sxs-lookup"><span data-stu-id="21cf2-149">`description`: UI help text indicating what the command does or how to use it.</span></span>
* <span data-ttu-id="21cf2-150">`parameters`: Включает все параметры, принимаемые командой (по крайней мере одна из них может иметь до пяти).</span><span class="sxs-lookup"><span data-stu-id="21cf2-150">`parameters`: Includes all parameters a command accepts (you must have at least one and can have up to five).</span></span>
* <span data-ttu-id="21cf2-151">`parameters.description`: Текст справки по пользовательскому интерфейсу, описывающий назначение параметра или пример ввода.</span><span class="sxs-lookup"><span data-stu-id="21cf2-151">`parameters.description`: UI help text describing the parameter's purpose or example input.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="21cf2-152">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="21cf2-152">App scaffolding</span></span>

<span data-ttu-id="21cf2-153">Формирование шаблонов приложений включает в себя `.env` файл, расположенный в корневом каталоге проекта, в котором ХРАНИТСЯ идентификатор и пароль для ленты расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="21cf2-153">The app scaffolding includes a `.env` file, located in the root directory of your project, which stores the ID and password of your messaging extension's bot.</span></span>

<span data-ttu-id="21cf2-154">Кроме того, в корневом каталоге существует `botActivityHandler.js` файл для обработки расширения системы обмена сообщениями (или техническим образом [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) ответа на поисковые запросы в Teams.</span><span class="sxs-lookup"><span data-stu-id="21cf2-154">Also in the root directory, there's a `botActivityHandler.js` file for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="21cf2-155">3. Настройка безопасного туннеля для приложения</span><span class="sxs-lookup"><span data-stu-id="21cf2-155">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="21cf2-156">В целях тестирования давайте разместите расширение обмена сообщениями на локальном веб-сервере (порт 3978).</span><span class="sxs-lookup"><span data-stu-id="21cf2-156">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="21cf2-157">В терминале запустите `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="21cf2-157">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="21cf2-158">Скопируйте URL-адрес HTTPS в выходных данных, так как teams требует HTTPS-подключения.</span><span class="sxs-lookup"><span data-stu-id="21cf2-158">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="21cf2-159">В `.publish` каталоге откройте `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="21cf2-159">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="21cf2-160">Замените `baseUrl0` значение скопированным URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="21cf2-160">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="21cf2-161">(Например, замените `baseUrl0=http://localhost:3000` на `baseUrl0=https://85528b2b3ca5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="21cf2-161">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="21cf2-162">Манифест приложения указывает на место размещения ленты, используемой расширением обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="21cf2-162">Your app manifest is pointing to where you're hosting the bot used by the messaging extension.</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="21cf2-163">4. Настройка Bot для расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="21cf2-163">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="21cf2-164">Расширения обмена сообщениями основываются на боты для отправки и обработки запросов пользователей из Teams в размещенную службу.</span><span class="sxs-lookup"><span data-stu-id="21cf2-164">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span>

<span data-ttu-id="21cf2-165">Робот должен быть зарегистрирован в службе Azure Bot, которая была выполнена при настройке приложения с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="21cf2-165">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

### <a name="specify-your-bot-id-and-password"></a><span data-ttu-id="21cf2-166">Указание идентификатора и пароля почтового робота</span><span class="sxs-lookup"><span data-stu-id="21cf2-166">Specify your bot ID and password</span></span>

<span data-ttu-id="21cf2-167">Когда ваш Bot зарегистрирован в службе Azure Bot, ему назначается идентификатор и пароль, о которых должно знать ваше приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="21cf2-167">When your bot is registered with the Azure Bot Service, it's assigned an ID and password that your Teams app must know about.</span></span>

1. <span data-ttu-id="21cf2-168">Нахождение идентификатора и пароля ленты, сохраненных во время установки набора средств.</span><span class="sxs-lookup"><span data-stu-id="21cf2-168">Locate the bot ID and password you stored during toolkit setup.</span></span>
1. <span data-ttu-id="21cf2-169">Откройте файл в корневом каталоге `.env` .</span><span class="sxs-lookup"><span data-stu-id="21cf2-169">In your root directory, open the `.env` file.</span></span>
1. <span data-ttu-id="21cf2-170">Задайте для идентификатора и пароля почтового робота `BotId` Свойства и пароль `BotPassword` соответственно.</span><span class="sxs-lookup"><span data-stu-id="21cf2-170">Set your bot ID and password to the `BotId` and `BotPassword` properties, respectively.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="21cf2-171">Добавление адреса конечной точки Bot</span><span class="sxs-lookup"><span data-stu-id="21cf2-171">Add the bot endpoint address</span></span>

<span data-ttu-id="21cf2-172">Необходимо указать URL-адрес конечной точки Bot для получения и обработки поисковых запросов в вашем расширении обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="21cf2-172">You must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="21cf2-173">Как правило, URL-адрес выглядит так `https://HOST_URL/api/messages` :</span><span class="sxs-lookup"><span data-stu-id="21cf2-173">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="21cf2-174">Это можно сделать быстро в наборе инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="21cf2-174">You can configure this quickly in the Teams Toolkit.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели действий, а затем выберите пункт **Открыть набор средств Microsoft Teams**.
1. <span data-ttu-id="21cf2-176">Перейдите к элементу **управления Bot > существующих регистраций ленты** и выберите элемент управления Bot, созданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="21cf2-176">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="21cf2-177">В поле **адрес конечной точки Bot** введите локальный веб-сервер, на котором размещается Bot ( `baseUrl10` значение), и добавьте `/api/messages` к нему.</span><span class="sxs-lookup"><span data-stu-id="21cf2-177">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot (`baseUrl10` value) and append `/api/messages` to it.</span></span>

<span data-ttu-id="21cf2-178">Ваш робот сможет обрабатывать запросы в вашем расширении системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="21cf2-178">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-run-your-app"></a><span data-ttu-id="21cf2-179">5. Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="21cf2-179">5. Run your app</span></span>

<span data-ttu-id="21cf2-180">Вы настроили URL-адрес для размещения своего расширения обмена сообщениями и настройки его для обработки запросов поиска.</span><span class="sxs-lookup"><span data-stu-id="21cf2-180">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="21cf2-181">Самое время заставить ваше приложение работать и работать.</span><span class="sxs-lookup"><span data-stu-id="21cf2-181">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="21cf2-182">В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .</span><span class="sxs-lookup"><span data-stu-id="21cf2-182">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="21cf2-183">Выполните команду `npm start` .</span><span class="sxs-lookup"><span data-stu-id="21cf2-183">Run `npm start`.</span></span>

<span data-ttu-id="21cf2-184">В случае успеха вы увидите нечто вроде следующего сообщения, указывающего на то, что служба расширения обмена сообщениями прослушивает активность `localhost` :</span><span class="sxs-lookup"><span data-stu-id="21cf2-184">If successful, you see something like the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="21cf2-185">6. Загрузка неопубликованных своего расширения обмена сообщениями в Teams</span><span class="sxs-lookup"><span data-stu-id="21cf2-185">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="21cf2-186">Если ваш модуль обмена сообщениями работает, вы можете установить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="21cf2-186">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="21cf2-187">Если вы еще не неопубликованные приложение Teams до и не выпустили проблемы, выполните указанные ниже [действия](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="21cf2-187">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="21cf2-188">Выполните вход в клиент Teams с учетной записью, позволяющей выполнять загрузку неопубликованных приложений.</span><span class="sxs-lookup"><span data-stu-id="21cf2-188">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="21cf2-189">Выберите **приложения**, а затем нажмите кнопку **Отправить пользовательское приложение**.</span><span class="sxs-lookup"><span data-stu-id="21cf2-189">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="21cf2-190">Перейдите в папку проекта приложения `.publish` и выберите `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="21cf2-190">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="21cf2-191">В модальном окне установки нажмите кнопку **Добавить** , чтобы установить приложение.</span><span class="sxs-lookup"><span data-stu-id="21cf2-191">In the install modal, select **Add** to install your app.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="21cf2-192">7. Тестирование расширения системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="21cf2-192">7. Test your messaging extension</span></span>

<span data-ttu-id="21cf2-193">Узнайте, как работают расширения обмена сообщениями в чате Teams.</span><span class="sxs-lookup"><span data-stu-id="21cf2-193">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="21cf2-194">Начните новый сеанс разговора.</span><span class="sxs-lookup"><span data-stu-id="21cf2-194">Start a new chat.</span></span> В поле создать **, а затем выберите** :::image type="icon" source="../assets/icons/teams-client-more.png"::: приложение расширения обмена сообщениями, которое вы только что неопубликованныее.<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-access.png" alt-text="Иллюстрация, на которой показано, как получить доступ к расширению системы обмена сообщениями на основе поиска в поле "Создание Teams".":::
1. <span data-ttu-id="21cf2-197">Попробуйте выполнить поиск чего-либо (например, "билеты").</span><span class="sxs-lookup"><span data-stu-id="21cf2-197">Try searching for something (for example, "Tickets").</span></span> <span data-ttu-id="21cf2-198">Если ваше приложение работает, вы увидите пример результатов поиска (вы можете добавить его позже).</span><span class="sxs-lookup"><span data-stu-id="21cf2-198">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Снимок экрана, демонстрирующий использование расширения обмена сообщениями на основе поиска в поле "Создание Teams".":::

## <a name="well-done"></a><span data-ttu-id="21cf2-200">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="21cf2-200">Well done</span></span>

<span data-ttu-id="21cf2-201">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="21cf2-201">Congratulations!</span></span> <span data-ttu-id="21cf2-202">У вас есть основные расширения системы обмена сообщениями Teams, которые задают поиск внешнего контента в поле "создать" или "команда".</span><span class="sxs-lookup"><span data-stu-id="21cf2-202">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21cf2-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="21cf2-203">Next steps</span></span>

<span data-ttu-id="21cf2-204">Чтобы продолжить и создать полнофункциональное расширение системы обмена сообщениями, ознакомьтесь со следующими страницами:</span><span class="sxs-lookup"><span data-stu-id="21cf2-204">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="21cf2-205">[Определите команды поиска](../messaging-extensions/how-to/search-commands/define-search-command.md) , связанные со службой.</span><span class="sxs-lookup"><span data-stu-id="21cf2-205">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="21cf2-206">Настройте службу для [реагирования на поиск пользователей](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span><span class="sxs-lookup"><span data-stu-id="21cf2-206">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="21cf2-207">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="21cf2-207">Troubleshooting</span></span>

<span data-ttu-id="21cf2-208">Приведенные ниже сведения помогут вам устранить проблемы, связанные с выполнением этого руководства.</span><span class="sxs-lookup"><span data-stu-id="21cf2-208">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="21cf2-209">Не удается установить набор средств</span><span class="sxs-lookup"><span data-stu-id="21cf2-209">Toolkit setup fails</span></span>

<span data-ttu-id="21cf2-210">Когда вы настраиваете проект приложения с помощью набора инструментов Teams, вы получаете сообщение об ошибке после выбора параметра **создать новый элемент Bot** и входа в систему с помощью учетной записи разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="21cf2-210">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="21cf2-211">Это может быть проблема проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="21cf2-211">This could be an authentication issue.</span></span> <span data-ttu-id="21cf2-212">Выполните следующие действия, чтобы завершить настройку проекта.</span><span class="sxs-lookup"><span data-stu-id="21cf2-212">Follow these steps to finish setting up your project.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели действий и нажмите **выйти**.
1. <span data-ttu-id="21cf2-214">Снова пройдите процесс настройки, выполнив вход в систему с той же учетной записью и создав новый элемент Bot.</span><span class="sxs-lookup"><span data-stu-id="21cf2-214">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="21cf2-215">Bot не подключены к Teams</span><span class="sxs-lookup"><span data-stu-id="21cf2-215">Bot isn't connected to Teams</span></span>

<span data-ttu-id="21cf2-216">Если вы установили приложение, но оно не работает, убедитесь, что линия канала для расширения обмена сообщениями [подключена к *каналу*команд службы Azure Bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="21cf2-216">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="21cf2-217">Важно понимать, что это не то же самое, что и канал в Teams.</span><span class="sxs-lookup"><span data-stu-id="21cf2-217">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="21cf2-218">В этом случае каналом является способ подключения службы Azure Bot к Teams или другому [поддерживаемому Microsoft или стороннему приложению для общения](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="21cf2-218">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="21cf2-219">Подробнее</span><span class="sxs-lookup"><span data-stu-id="21cf2-219">Learn more</span></span>

* [<span data-ttu-id="21cf2-220">Включение функции Link унфурлинг</span><span class="sxs-lookup"><span data-stu-id="21cf2-220">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="21cf2-221">Добавить аутентификацию</span><span class="sxs-lookup"><span data-stu-id="21cf2-221">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="21cf2-222">Создание расширения обмена сообщениями на основе действий</span><span class="sxs-lookup"><span data-stu-id="21cf2-222">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="21cf2-223">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="21cf2-223">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
