### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="6de75-101">Используйте App Studio для обновления пакета приложений</span><span class="sxs-lookup"><span data-stu-id="6de75-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="6de75-102">App Studio это Teams приложение, которое вы можете установить Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="6de75-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="6de75-103">Упрощает создание и регистрацию приложения.</span><span class="sxs-lookup"><span data-stu-id="6de75-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="6de75-104">Выполните следующие шаги по обновлению пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="6de75-104">Complete the following steps to update the app package:</span></span>

1. <span data-ttu-id="6de75-105">Чтобы установить App Studio Teams, выберите **значок Apps** в нижней части левой бара и ищите **App Studio:**</span><span class="sxs-lookup"><span data-stu-id="6de75-105">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**:</span></span>

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. <span data-ttu-id="6de75-106">Выберите **плитку App Studio** и выберите **Установку.**</span><span class="sxs-lookup"><span data-stu-id="6de75-106">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="6de75-107">App Studio установлен:</span><span class="sxs-lookup"><span data-stu-id="6de75-107">The App Studio is installed:</span></span>

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. <span data-ttu-id="6de75-108">Чтобы создать пакет приложений для вашего Teams приложения, выберите **вкладку редактора Manifest** в **App Studio:**</span><span class="sxs-lookup"><span data-stu-id="6de75-108">To create the app package for your Teams app, select the **Manifest editor** tab in **App Studio**:</span></span>

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    <span data-ttu-id="6de75-109">Образец поставляется со своим манифестом и предназначен для создания пакета приложений при построении проекта.</span><span class="sxs-lookup"><span data-stu-id="6de75-109">The sample comes with its own manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="6de75-110">На .NET это делается Visual Studio и Node.js это делается путем `gulp` ввода на командной строке в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="6de75-110">On .NET this is done in Visual Studio and on Node.js this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

    ```bash
    $ gulp
    [13:39:27] Using gulpfile ~\documents\github\msteams-samples-hello-world-nodejs\gulpfile.js
    [13:39:27] Starting 'clean'...
    [13:39:27] Starting 'generate-manifest'...
    [13:39:27] Finished 'generate-manifest' after 11 ms
    [13:39:27] Finished 'clean' after 21 ms
    [13:39:27] Starting 'default'...
    Build completed. Output in manifest folder
    [13:39:27] Finished 'default' after 62 μs
    ```

    <span data-ttu-id="6de75-111">Имя сгенерированного пакета приложений **helloworldapp.zip.**</span><span class="sxs-lookup"><span data-stu-id="6de75-111">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="6de75-112">Вы можете искать этот файл, если местоположение не ясно в инструменте, который вы используете.</span><span class="sxs-lookup"><span data-stu-id="6de75-112">You can search for this file if the location is not clear in the tool you are using.</span></span>

1. <span data-ttu-id="6de75-113">Теперь, чтобы изменить этот пакет приложений, **выберите Импорт существующего** приложения в **редакторе Manifest:**</span><span class="sxs-lookup"><span data-stu-id="6de75-113">Now to modify this app package, select **Import an existing app** in the **Manifest editor**:</span></span>

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. <span data-ttu-id="6de75-114">Выберите **плитку Hello World** для недавно импортированного приложения:</span><span class="sxs-lookup"><span data-stu-id="6de75-114">Select the **Hello World** tile for your newly imported app:</span></span>

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="6de75-115">На следующем изображении показан импортный пакет приложений в App Studio:</span><span class="sxs-lookup"><span data-stu-id="6de75-115">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="6de75-116">На левой стороне редактора Manifest есть список шагов.</span><span class="sxs-lookup"><span data-stu-id="6de75-116">On the left-hand side of the Manifest editor there is a list of steps.</span></span> <span data-ttu-id="6de75-117">С правой стороны есть список свойств, которые должны быть заполнены для каждого шага.</span><span class="sxs-lookup"><span data-stu-id="6de75-117">On the right-hand side there is a list of properties that need to be filled in for each step.</span></span> <span data-ttu-id="6de75-118">Когда вы начали с образца приложения, большая часть информации уже завершена.</span><span class="sxs-lookup"><span data-stu-id="6de75-118">As you started with a sample app, much of the information is already completed.</span></span> <span data-ttu-id="6de75-119">Следующие шаги позволяют обновить свойства приложения Hello World.</span><span class="sxs-lookup"><span data-stu-id="6de75-119">The next steps enable you to update the properties of the Hello World app.</span></span>

#### <a name="app-details"></a><span data-ttu-id="6de75-120">Подробная информация о приложении</span><span class="sxs-lookup"><span data-stu-id="6de75-120">App details</span></span>

<span data-ttu-id="6de75-121">Выберите **детали приложения в подробном** **состоянии**.</span><span class="sxs-lookup"><span data-stu-id="6de75-121">Select **App details** under **Details**.</span></span> <span data-ttu-id="6de75-122">Выберите **кнопку** Generate для создания нового идентификатора App ID.</span><span class="sxs-lookup"><span data-stu-id="6de75-122">Select the **Generate** button to create a new App ID.</span></span>

<span data-ttu-id="6de75-123">Ваш новый идентификатор App похож на `2322041b-72bf-459d-b107-f4f335bc35bd` .</span><span class="sxs-lookup"><span data-stu-id="6de75-123">Your new App ID is similar to `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="6de75-124">Пройдитесь по деталям приложения в правом стекле, включая информацию **разработчика и сведения** **о брендинге.**</span><span class="sxs-lookup"><span data-stu-id="6de75-124">Go through the app details in the right-hand pane including **Developer information** and **Branding** details.</span></span> <span data-ttu-id="6de75-125">Эти детали важны, если вы пишете новое приложение для распространения.</span><span class="sxs-lookup"><span data-stu-id="6de75-125">These details are important if you are writing a new app for distribution.</span></span>

#### <a name="tabs"></a><span data-ttu-id="6de75-126">Вкладки</span><span class="sxs-lookup"><span data-stu-id="6de75-126">Tabs</span></span>

<span data-ttu-id="6de75-127">Просто добавить вкладки в приложение Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="6de75-127">It is simple to add tabs to a Teams app.</span></span> <span data-ttu-id="6de75-128">Пример приложения уже поддерживает несколько вкладок, и вы можете включить их.</span><span class="sxs-lookup"><span data-stu-id="6de75-128">The sample app already supports several tabs, and you can enable them.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="6de75-129">Вкладка команды</span><span class="sxs-lookup"><span data-stu-id="6de75-129">Team tab</span></span>

<span data-ttu-id="6de75-130">Ваше приложение может иметь только одну вкладку Team:</span><span class="sxs-lookup"><span data-stu-id="6de75-130">Your app can only have one Team tab:</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="6de75-131">В этом примере отображается вкладка Team.</span><span class="sxs-lookup"><span data-stu-id="6de75-131">In this sample, the Team tab is where your configuration page is displayed.</span></span> <span data-ttu-id="6de75-132">Выберите **символ** URL **конфигурации Tab и** выберите **Редактировать** из выпадают меню.</span><span class="sxs-lookup"><span data-stu-id="6de75-132">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="6de75-133">Измените URL-адрес `https://yourteamsapp.ngrok.io/configure` на `yourteamsapp.ngrok.io` URL-адрес, где он должен быть заменен URL-адресом, который [использовался при размещении приложения.](#host-the-sample-app)</span><span class="sxs-lookup"><span data-stu-id="6de75-133">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` must be replaced with the URL that you used when [hosting your app](#host-the-sample-app).</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="6de75-134">Личные вкладки</span><span class="sxs-lookup"><span data-stu-id="6de75-134">Personal tabs</span></span>

<span data-ttu-id="6de75-135">Ваше приложение может иметь до 16 вкладок, включая вкладку Team.</span><span class="sxs-lookup"><span data-stu-id="6de75-135">Your app can have up to 16 tabs, including the Team tab.</span></span>

<span data-ttu-id="6de75-136">Личные вкладки отличаются от вкладки **Team. Hello Tab** уже указан в личном списке вкладок со значением заполнителя. `com.contoso.helloworld.hellotab`</span><span class="sxs-lookup"><span data-stu-id="6de75-136">Personal tabs are different from the Team tab. **Hello Tab** is already listed in the personal tabs list with a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="6de75-137">Выберите **символ** URL **конфигурации Tab и** выберите **Редактировать** из выпадают меню.</span><span class="sxs-lookup"><span data-stu-id="6de75-137">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="6de75-138">Появляется следующее диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="6de75-138">The following dialog box appears:</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="6de75-139">Обновление следующих коробок с URL-адресом приложения:</span><span class="sxs-lookup"><span data-stu-id="6de75-139">Update the following boxes with your app URL:</span></span>

- <span data-ttu-id="6de75-140">Изменение **url-адреса содержимого** на `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="6de75-140">Change the **Content URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="6de75-141">Изменение **URL-адреса веб-сайта** на `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="6de75-141">Change the **Website URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="6de75-142">Замените `yourteamsapp.ngrok.io` URL-адрес, который вы использовали при размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="6de75-142">Replace `yourteamsapp.ngrok.io` by the URL that you used when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="6de75-143">Боты</span><span class="sxs-lookup"><span data-stu-id="6de75-143">Bots</span></span>

<span data-ttu-id="6de75-144">Легко добавить функциональность ботов в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="6de75-144">It is easy to add the bots functionality to your app.</span></span> <span data-ttu-id="6de75-145">В **примере** приложения Hello World уже есть бот как часть образца, но вы должны зарегистрировать его в корпорации Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="6de75-145">The **Hello World** sample app already has a bot as part of the sample, but you must register it with Microsoft:</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="6de75-146">Бот, который был импортирован из образца, не имеет связанного идентификатора App ID.</span><span class="sxs-lookup"><span data-stu-id="6de75-146">The bot that was imported from the sample does not have an associated App ID.</span></span> <span data-ttu-id="6de75-147">Вы должны создать нового бота, чтобы App Studio можно было создать новый идентификатор App ID и зарегистрировать его в корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6de75-147">You must create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span>

> [!NOTE]
> <span data-ttu-id="6de75-148">Идентификатор App, созданный App Studio для бота, отличается от идентификатора App ID, созданного для приложения.</span><span class="sxs-lookup"><span data-stu-id="6de75-148">The App ID created by App Studio for the bot is different from the App ID created for the app.</span></span> <span data-ttu-id="6de75-149">Каждый бот в приложении требует своего идентификатора App ID.</span><span class="sxs-lookup"><span data-stu-id="6de75-149">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="6de75-150">Выполните следующие шаги по настройке бота:</span><span class="sxs-lookup"><span data-stu-id="6de75-150">Complete the following steps to setup your bot:</span></span>

1. <span data-ttu-id="6de75-151">Выберите **Удалить** рядом с импортированным ботом в списке ботов.</span><span class="sxs-lookup"><span data-stu-id="6de75-151">Select **Delete** next to the imported bot in the bot list.</span></span> <span data-ttu-id="6de75-152">Теперь нет ботов осталось показать.</span><span class="sxs-lookup"><span data-stu-id="6de75-152">Now there are no bots left to show.</span></span> 
1. <span data-ttu-id="6de75-153">Выберите **настройку** для **отображения диалогового окна** Для бота.</span><span class="sxs-lookup"><span data-stu-id="6de75-153">Select **Setup** to display the **Set up a bot** dialog box.</span></span>

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. <span data-ttu-id="6de75-154">Добавьте бот имя **Contoso бот и** выберите все три чек-боксы под **областью.**</span><span class="sxs-lookup"><span data-stu-id="6de75-154">Add a bot name **Contoso bot** and select all three check boxes under **Scope**.</span></span>
1. <span data-ttu-id="6de75-155">Выберите **Сохранить,** чтобы выйти из диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="6de75-155">Choose **Save** to exit the dialog box.</span></span> <span data-ttu-id="6de75-156">App Studio регистрирует вашего бота в корпорации Майкрософт и отображает ваш новый бот в списке ботов.</span><span class="sxs-lookup"><span data-stu-id="6de75-156">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> 
1. <span data-ttu-id="6de75-157">Теперь откройте текстовый файл в блокноте и скопировать и вставить свой новый идентификатор бота в него.</span><span class="sxs-lookup"><span data-stu-id="6de75-157">Now open a text file in notepad and copy and paste your new bot ID into it.</span></span>
1. <span data-ttu-id="6de75-158">Нажмите **Generate New Password** и обратите внимание на пароль в том же текстовом файле, который вы отметили в идентификаторе приложения бота.</span><span class="sxs-lookup"><span data-stu-id="6de75-158">Click **Generate New Password**, and note the password in the same text file you noted your bot App ID.</span></span>
1. <span data-ttu-id="6de75-159">**Обновите адрес конечной точки** `https://yourteamsapp.ngrok.io/api/messages` Bot и `yourteamsapp.ngrok.io` замените URL-адрес, который вы использовали при размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="6de75-159">Update the **Bot endpoint address** to `https://yourteamsapp.ngrok.io/api/messages`, and replace `yourteamsapp.ngrok.io` with the URL that you used when hosting your app.</span></span>
1. <span data-ttu-id="6de75-160">Теперь сохраните текстовый файл, поскольку вы должны добавить информацию из файла в ваше приложение для хостинга, чтобы обеспечить безопасную связь с ботом.</span><span class="sxs-lookup"><span data-stu-id="6de75-160">Now save your text file as you must add the information from the file to your hosted app to allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="6de75-161">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="6de75-161">Messaging extensions</span></span>

<span data-ttu-id="6de75-162">Расширения сообщений позволяют пользователям запрашивать информацию из вашего сервиса и размещать эту информацию.</span><span class="sxs-lookup"><span data-stu-id="6de75-162">Messaging extensions let users ask for information from your service and post that information.</span></span> <span data-ttu-id="6de75-163">Информация размещена в виде карт в разговоре канала.</span><span class="sxs-lookup"><span data-stu-id="6de75-163">The information is posted in the form of cards into the channel conversation.</span></span> <span data-ttu-id="6de75-164">Расширения сообщений отображаются в нижней части окна compose.</span><span class="sxs-lookup"><span data-stu-id="6de75-164">Messaging extensions appear at the bottom of the compose box.</span></span>

<span data-ttu-id="6de75-165">Выполните следующие шаги по настройке расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="6de75-165">Complete the following steps to setup your messaging extension:</span></span>

1. <span data-ttu-id="6de75-166">Выберите **расширения обмена** **сообщениями под** возможностями в левом стекле App Studio для настройки расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="6de75-166">Select **Messaging extensions** under **Capabilities** in the left-hand pane of App Studio to configure the messaging extension:</span></span>

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    <span data-ttu-id="6de75-167">Пример расширения обмена сообщениями указан в **панели расширения сообщений.**</span><span class="sxs-lookup"><span data-stu-id="6de75-167">The sample messaging extension is listed in the **Messaging Extensions** pane.</span></span>

1. <span data-ttu-id="6de75-168">Выберите **Удалить,** чтобы удалить расширение обмена сообщениями, **выберите Настройка,** и следовать тем же шагам, используемым [для ботов.](#bots)</span><span class="sxs-lookup"><span data-stu-id="6de75-168">Select **Delete** to remove the messaging extension, select **Set up**, and follow the same steps used for [bots](#bots).</span></span> <span data-ttu-id="6de75-169">Отображается диалоговое окно Messaging **Extension.**</span><span class="sxs-lookup"><span data-stu-id="6de75-169">The **Messaging Extension** dialog box is displayed.</span></span>
1. <span data-ttu-id="6de75-170">Выберите **существующую вкладку бота** и **выберите одного из моих существующих ботов.**</span><span class="sxs-lookup"><span data-stu-id="6de75-170">Select the **Use existing bot** tab and **Select from one of my existing bots**.</span></span>
1. <span data-ttu-id="6de75-171">Выберите бота, созданного из выпадают из меню.</span><span class="sxs-lookup"><span data-stu-id="6de75-171">Select the bot you created from the drop-down menu.</span></span> <span data-ttu-id="6de75-172">Добавьте **имя Bot и** выберите **Сохранить,** чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="6de75-172">Add a **Bot name** and select **Save** to close the dialog box.</span></span>
1. <span data-ttu-id="6de75-173">В разделе **Командование** выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6de75-173">Under the **Command** section, select **Add**.</span></span> <span data-ttu-id="6de75-174">Чтобы добавить команду на основе поиска, выберите **Разрешить пользователям запрашивать вашу службу для получения информации и вставить ее в опцию сообщения.**</span><span class="sxs-lookup"><span data-stu-id="6de75-174">To add a search-based command, select the **Allow users to query your service for information and insert that into a message** option.</span></span>
1. <span data-ttu-id="6de75-175">В новом **диалоговом** поле команды введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="6de75-175">In the **New command** dialog box, enter the following values:</span></span>

    <span data-ttu-id="6de75-176">Под **новым командованием**:</span><span class="sxs-lookup"><span data-stu-id="6de75-176">Under **New command**:</span></span>

    - <span data-ttu-id="6de75-177">**Идентификатор команды**: Введите случайный текст</span><span class="sxs-lookup"><span data-stu-id="6de75-177">**Command ID**: Enter random text</span></span>
    - <span data-ttu-id="6de75-178">**Название**: Введите случайное название</span><span class="sxs-lookup"><span data-stu-id="6de75-178">**Title**: Enter random title</span></span>
    - <span data-ttu-id="6de75-179">**Описание /** описание : Введите случайное описание</span><span class="sxs-lookup"><span data-stu-id="6de75-179">**Description**: Enter random description</span></span>

    <span data-ttu-id="6de75-180">В **соответствии с параметром**:</span><span class="sxs-lookup"><span data-stu-id="6de75-180">Under **Parameter**:</span></span>

    - <span data-ttu-id="6de75-181">**Имя**: Введите имя параметра</span><span class="sxs-lookup"><span data-stu-id="6de75-181">**Name**: Enter the parameter name</span></span>
    - <span data-ttu-id="6de75-182">**Название**: Введите название карты</span><span class="sxs-lookup"><span data-stu-id="6de75-182">**Title**: Enter the card title</span></span>
    - <span data-ttu-id="6de75-183">**Описание**/ см. Описание : Введите описание карты</span><span class="sxs-lookup"><span data-stu-id="6de75-183">**Description**: Enter card description</span></span>

1. <span data-ttu-id="6de75-184">После вставки информации выберите **Сохранить,** чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="6de75-184">After you enter the information, select **Save** to close the dialog box.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="6de75-185">Зарегистрируйте приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="6de75-185">Register your app in Teams</span></span>

<span data-ttu-id="6de75-186">После ввода деталей приложения выполните следующие шаги по регистрации приложения в Teams:</span><span class="sxs-lookup"><span data-stu-id="6de75-186">After entering the details of your app, complete the following steps to register your app in Teams:</span></span>

1. <span data-ttu-id="6de75-187">Используйте **тест и распространение** App Studio для установки приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="6de75-187">Use **Test and distribute** of App Studio to install your app in Teams.</span></span> 
1. <span data-ttu-id="6de75-188">Обновите размещенную заявку с помощью идентификатора приложения и пароля для бота.</span><span class="sxs-lookup"><span data-stu-id="6de75-188">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="6de75-189">Для образца приложения используйте тот же идентификатор App ID и пароль как для бота, так и для расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="6de75-189">For the sample app, use the same App ID and password for both bot and messaging extension.</span></span> 
1. <span data-ttu-id="6de75-190">Выберите **тест и** **распределите** под отделкой в левом стекле App Studio:</span><span class="sxs-lookup"><span data-stu-id="6de75-190">Select **Test and distribute**  under **Finish** in the left-hand pane of App Studio:</span></span>

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. <span data-ttu-id="6de75-191">Чтобы загрузить приложение в Teams, выберите кнопку **«Установить»** в рамках **тестирования и распространения:**</span><span class="sxs-lookup"><span data-stu-id="6de75-191">To upload your app to Teams, select the **Install** button under **Test and Distribute**:</span></span>

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

1. <span data-ttu-id="6de75-192">Выберите **поле** поиска в **разделе Добавить в раздел команды** и выберите команду для добавления образца приложения.</span><span class="sxs-lookup"><span data-stu-id="6de75-192">Select the **Search** box in the **Add to a team** section and select a team to add the sample app.</span></span> <span data-ttu-id="6de75-193">Вы можете создать специальную группу для тестирования.</span><span class="sxs-lookup"><span data-stu-id="6de75-193">You can set up a special team for testing.</span></span>
1. <span data-ttu-id="6de75-194">Выберите **кнопку** «Установить» в нижней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="6de75-194">Select the **Install** button at the bottom of the dialog box.</span></span>

<span data-ttu-id="6de75-195">Ваше приложение теперь доступно в Teams.</span><span class="sxs-lookup"><span data-stu-id="6de75-195">Your app is now available in Teams.</span></span> <span data-ttu-id="6de75-196">Тем не менее, бот и расширение обмена сообщениями не будут работать до тех пор, пока вы не обновите среду размещенных приложений с помощью ID и паролей App.</span><span class="sxs-lookup"><span data-stu-id="6de75-196">However, the bot and the messaging extension will not work until you update the hosted applications environment with the App IDs and passwords.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
