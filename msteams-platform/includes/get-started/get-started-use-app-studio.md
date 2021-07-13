### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="64029-101">Используйте App Studio для обновления пакета приложений</span><span class="sxs-lookup"><span data-stu-id="64029-101">Use App Studio to update the app package</span></span>

> [!TIP]
> <span data-ttu-id="64029-102">**Попробуйте портал разработчика:** App Studio вскоре будет отвягот.</span><span class="sxs-lookup"><span data-stu-id="64029-102">**Try the Developer Portal**: App Studio will soon be depricated.</span></span> <span data-ttu-id="64029-103">Настройка, распространение и управление Teams приложениями с помощью нового [портала разработчиков.](https://dev.teams.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="64029-103">Configure, distribute, and manage your Teams apps with the new [Developer Portal](https://dev.teams.microsoft.com/).</span></span>

<span data-ttu-id="64029-104">App Studio — это Teams приложение, которое можно установить из Teams магазина.</span><span class="sxs-lookup"><span data-stu-id="64029-104">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="64029-105">Это упрощает создание и регистрацию приложения.</span><span class="sxs-lookup"><span data-stu-id="64029-105">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="64029-106">Выполните следующие действия по обновлению пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="64029-106">Complete the following steps to update the app package:</span></span>

1. <span data-ttu-id="64029-107">Чтобы установить App Studio в Teams, выберите значок **Apps** в нижней части левой панели и выберите **App Studio:**</span><span class="sxs-lookup"><span data-stu-id="64029-107">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**:</span></span>

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. <span data-ttu-id="64029-108">Выберите **плитку App Studio** и **установите**.</span><span class="sxs-lookup"><span data-stu-id="64029-108">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="64029-109">Установлена App Studio:</span><span class="sxs-lookup"><span data-stu-id="64029-109">The App Studio is installed:</span></span>

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. <span data-ttu-id="64029-110">Чтобы создать пакет приложений для Teams, выберите вкладку **Редактор Манифеста** в **App Studio:**</span><span class="sxs-lookup"><span data-stu-id="64029-110">To create the app package for your Teams app, select the **Manifest editor** tab in **App Studio**:</span></span>

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>


    <span data-ttu-id="64029-111">Пример поставляется с собственным манифестом и предназначен для создания пакета приложений при построении проекта.</span><span class="sxs-lookup"><span data-stu-id="64029-111">The sample comes with its own manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="64029-112">На сайте .NET manifest.jsфайл может быть расположен в Visual Studio в Манифесте ```Microsoft.Teams.Samples.HelloWorld.Web``` под .</span><span class="sxs-lookup"><span data-stu-id="64029-112">On .NET, the manifest.json file can be located in Visual Studio in Manifest under ```Microsoft.Teams.Samples.HelloWorld.Web```.</span></span> <span data-ttu-id="64029-113">В Node.js это делается путем ввода в строку команды в корневом `gulp` каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="64029-113">On Node.js, this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

     <span data-ttu-id="64029-114">В Visual Studio, manifest.jsфайл находится в соответствии с **манифестом** `Microsoft.Teams.Samples.HelloWorld.Web` в .</span><span class="sxs-lookup"><span data-stu-id="64029-114">In Visual Studio, the manifest.json file is located in under **Manifest** in `Microsoft.Teams.Samples.HelloWorld.Web`.</span></span> <span data-ttu-id="64029-115">Этот шаг описывается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="64029-115">This step is described by the following image:</span></span>  
    
    <img  width="450px" alt="Build the app package on .NET with Visual Studio" src="~/assets/images/get-started/app-package-on-.NET-with-Visual-Studio.png"/>
    
    <span data-ttu-id="64029-116">Вы можете создать пакет приложений на Node.js, введя в строку команды в корневом `gulp` каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="64029-116">You can build the app package on Node.js by typing `gulp` at the command line in the root directory of the project.</span></span>


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

    <span data-ttu-id="64029-117">Имя сгенерированного пакета приложений **helloworldapp.zip**.</span><span class="sxs-lookup"><span data-stu-id="64029-117">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="64029-118">Этот файл можно искать, если в используемом средстве расположение не ясно.</span><span class="sxs-lookup"><span data-stu-id="64029-118">You can search for this file if the location is not clear in the tool you are using.</span></span>

1. <span data-ttu-id="64029-119">Чтобы изменить этот пакет приложений, выберите **импорт существующего** приложения в **редакторе Manifest:**</span><span class="sxs-lookup"><span data-stu-id="64029-119">Now to modify this app package, select **Import an existing app** in the **Manifest editor**:</span></span>

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. <span data-ttu-id="64029-120">Выберите **плитку Hello World** для вашего недавно импортируемого приложения:</span><span class="sxs-lookup"><span data-stu-id="64029-120">Select the **Hello World** tile for your newly imported app:</span></span>

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

    <span data-ttu-id="64029-121">На следующем изображении показан импортируемый пакет приложений в App Studio:</span><span class="sxs-lookup"><span data-stu-id="64029-121">The following image shows the imported app package in App Studio:</span></span>

    <img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

    <span data-ttu-id="64029-122">На левой стороне редактора Манифеста находится список действий.</span><span class="sxs-lookup"><span data-stu-id="64029-122">On the left-hand side of the Manifest editor there is a list of steps.</span></span> <span data-ttu-id="64029-123">В правой части имеется список свойств, которые необходимо заполнить для каждого шага.</span><span class="sxs-lookup"><span data-stu-id="64029-123">On the right-hand side there is a list of properties that need to be filled in for each step.</span></span> <span data-ttu-id="64029-124">По мере начала работы с примерным приложением большая часть сведений уже завершена.</span><span class="sxs-lookup"><span data-stu-id="64029-124">As you started with a sample app, much of the information is already completed.</span></span> <span data-ttu-id="64029-125">Следующие действия позволяют обновить свойства приложения Hello World.</span><span class="sxs-lookup"><span data-stu-id="64029-125">The next steps enable you to update the properties of the Hello World app.</span></span>

#### <a name="app-details"></a><span data-ttu-id="64029-126">Сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="64029-126">App details</span></span>

<span data-ttu-id="64029-127">Выберите **сведения о приложении** в **статье Details**.</span><span class="sxs-lookup"><span data-stu-id="64029-127">Select **App details** under **Details**.</span></span> <span data-ttu-id="64029-128">Выберите **кнопку Создать,** чтобы создать новый ID приложения.</span><span class="sxs-lookup"><span data-stu-id="64029-128">Select the **Generate** button to create a new App ID.</span></span>

<span data-ttu-id="64029-129">Ваш новый ID приложения похож на `2322041b-72bf-459d-b107-f4f335bc35bd` .</span><span class="sxs-lookup"><span data-stu-id="64029-129">Your new App ID is similar to `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="64029-130">Сведения о приложении в правой области, включая сведения **разработчика** и **сведения о брендинге.**</span><span class="sxs-lookup"><span data-stu-id="64029-130">Go through the app details in the right-hand pane including **Developer information** and **Branding** details.</span></span> <span data-ttu-id="64029-131">Эти сведения важны, если вы пишете новое приложение для распространения.</span><span class="sxs-lookup"><span data-stu-id="64029-131">These details are important if you are writing a new app for distribution.</span></span>

#### <a name="tabs"></a><span data-ttu-id="64029-132">Вкладки</span><span class="sxs-lookup"><span data-stu-id="64029-132">Tabs</span></span>

<span data-ttu-id="64029-133">Просто добавить вкладки в приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="64029-133">It is simple to add tabs to a Teams app.</span></span> <span data-ttu-id="64029-134">Пример приложения уже поддерживает несколько вкладок, и вы можете включить их.</span><span class="sxs-lookup"><span data-stu-id="64029-134">The sample app already supports several tabs, and you can enable them.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="64029-135">Вкладка Team</span><span class="sxs-lookup"><span data-stu-id="64029-135">Team tab</span></span>

<span data-ttu-id="64029-136">В приложении может быть только одна вкладка Team:</span><span class="sxs-lookup"><span data-stu-id="64029-136">Your app can only have one Team tab:</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="64029-137">В этом примере вкладка Team отображает страницу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="64029-137">In this sample, the Team tab is where your configuration page is displayed.</span></span> <span data-ttu-id="64029-138">Выберите **символ url-адреса** конфигурации **Tab** и выберите **Изменить** из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="64029-138">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="64029-139">Измените URL-адрес на то, где необходимо заменить URL-адрес, используемый при `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="64029-139">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` must be replaced with the URL that you used when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="64029-140">Личные вкладки</span><span class="sxs-lookup"><span data-stu-id="64029-140">Personal tabs</span></span>

<span data-ttu-id="64029-141">В вашем приложении может быть до 16 вкладок, включая вкладку Team.</span><span class="sxs-lookup"><span data-stu-id="64029-141">Your app can have up to 16 tabs, including the Team tab.</span></span>

<span data-ttu-id="64029-142">Личные вкладки отличаются от вкладки **Team. Вкладка Hello уже** указана в списке личных вкладок со значением места. `com.contoso.helloworld.hellotab`</span><span class="sxs-lookup"><span data-stu-id="64029-142">Personal tabs are different from the Team tab. **Hello Tab** is already listed in the personal tabs list with a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="64029-143">Выберите **символ url-адреса** конфигурации **Tab** и выберите **Изменить** из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="64029-143">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="64029-144">Появится следующее диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="64029-144">The following dialog box appears:</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="64029-145">Обновление следующих полей с URL-адресом приложения:</span><span class="sxs-lookup"><span data-stu-id="64029-145">Update the following boxes with your app URL:</span></span>

- <span data-ttu-id="64029-146">Измените **поле URL-адреса контента** на `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="64029-146">Change the **Content URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="64029-147">Изменение **URL-адреса веб-сайта** на `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="64029-147">Change the **Website URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="64029-148">Замените `yourteamsapp.ngrok.io` URL-адрес, используемый при размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="64029-148">Replace `yourteamsapp.ngrok.io` by the URL that you used when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="64029-149">Боты</span><span class="sxs-lookup"><span data-stu-id="64029-149">Bots</span></span>

<span data-ttu-id="64029-150">Легко добавить функции ботов в приложение.</span><span class="sxs-lookup"><span data-stu-id="64029-150">It is easy to add the bots functionality to your app.</span></span> <span data-ttu-id="64029-151">В **примере Приложения Hello World** уже есть бот в качестве части примера, но его необходимо зарегистрировать в Корпорации Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="64029-151">The **Hello World** sample app already has a bot as part of the sample, but you must register it with Microsoft:</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="64029-152">У бота, импортируемого из примера, нет связанного СД приложения.</span><span class="sxs-lookup"><span data-stu-id="64029-152">The bot that was imported from the sample does not have an associated App ID.</span></span> <span data-ttu-id="64029-153">Необходимо создать новый бот, чтобы App Studio создал новый ID приложения и зарегистрировал его в Корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="64029-153">You must create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span>

> [!NOTE]
> <span data-ttu-id="64029-154">ID приложения, созданный App Studio для бота, отличается от ID приложения, созданного для приложения.</span><span class="sxs-lookup"><span data-stu-id="64029-154">The App ID created by App Studio for the bot is different from the App ID created for the app.</span></span> <span data-ttu-id="64029-155">Каждому боту в приложении требуется свой собственный ID приложения.</span><span class="sxs-lookup"><span data-stu-id="64029-155">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="64029-156">Выполните следующие действия по настройке бота:</span><span class="sxs-lookup"><span data-stu-id="64029-156">Complete the following steps to setup your bot:</span></span>

1. <span data-ttu-id="64029-157">Выберите **Удаление** рядом с импортируемым ботом в списке ботов.</span><span class="sxs-lookup"><span data-stu-id="64029-157">Select **Delete** next to the imported bot in the bot list.</span></span> <span data-ttu-id="64029-158">Теперь для показа не осталось ботов.</span><span class="sxs-lookup"><span data-stu-id="64029-158">Now there are no bots left to show.</span></span> 
1. <span data-ttu-id="64029-159">Выберите **Установку,** чтобы **отобразить диалоговое** окно "Настройка бота".</span><span class="sxs-lookup"><span data-stu-id="64029-159">Select **Setup** to display the **Set up a bot** dialog box.</span></span>

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. <span data-ttu-id="64029-160">Добавьте бот с именем **бота Contoso** и выберите все три флажка в **области.**</span><span class="sxs-lookup"><span data-stu-id="64029-160">Add a bot name **Contoso bot** and select all three check boxes under **Scope**.</span></span>
1. <span data-ttu-id="64029-161">Выберите **Сохранить,** чтобы выйти из диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="64029-161">Choose **Save** to exit the dialog box.</span></span> <span data-ttu-id="64029-162">App Studio регистрирует бот в Microsoft и отображает новый бот в списке ботов.</span><span class="sxs-lookup"><span data-stu-id="64029-162">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> 
1. <span data-ttu-id="64029-163">Теперь откройте текстовый файл в блокноте и скопируйте и вклейте в него новый бот-ИД.</span><span class="sxs-lookup"><span data-stu-id="64029-163">Now open a text file in notepad and copy and paste your new bot ID into it.</span></span>
1. <span data-ttu-id="64029-164">Нажмите **кнопку Создание нового пароля** и обратите внимание на пароль в том же текстовом файле, который вы отметили в коде бота App.</span><span class="sxs-lookup"><span data-stu-id="64029-164">Click **Generate New Password**, and note the password in the same text file you noted your bot App ID.</span></span>
1. <span data-ttu-id="64029-165">**Обновите адрес конечной точки Bot** и замените URL-адресом, используемым при `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="64029-165">Update the **Bot endpoint address** to `https://yourteamsapp.ngrok.io/api/messages`, and replace `yourteamsapp.ngrok.io` with the URL that you used when hosting your app.</span></span>
1. <span data-ttu-id="64029-166">Теперь сохраните текстовый файл, так как вы должны добавить сведения из файла в ваше хост-приложение, чтобы обеспечить безопасное общение с ботом.</span><span class="sxs-lookup"><span data-stu-id="64029-166">Now save your text file as you must add the information from the file to your hosted app to allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="64029-167">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="64029-167">Messaging extensions</span></span>

<span data-ttu-id="64029-168">Расширения обмена сообщениями позволяет пользователям запросить сведения из вашей службы и опубликовать эти сведения.</span><span class="sxs-lookup"><span data-stu-id="64029-168">Messaging extensions let users ask for information from your service and post that information.</span></span> <span data-ttu-id="64029-169">Сведения вывешиты в виде карточек в диалог канала.</span><span class="sxs-lookup"><span data-stu-id="64029-169">The information is posted in the form of cards into the channel conversation.</span></span> <span data-ttu-id="64029-170">Расширения обмена сообщениями отображаются в нижней части окна составить.</span><span class="sxs-lookup"><span data-stu-id="64029-170">Messaging extensions appear at the bottom of the compose box.</span></span>

<span data-ttu-id="64029-171">Выполните следующие действия по настройке расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="64029-171">Complete the following steps to setup your messaging extension:</span></span>

1. <span data-ttu-id="64029-172">Выберите **расширения обмена сообщениями** в соответствии с **возможностями** в левом окантовке App Studio для настройки расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="64029-172">Select **Messaging extensions** under **Capabilities** in the left-hand pane of App Studio to configure the messaging extension:</span></span>

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    <span data-ttu-id="64029-173">Расширение примера обмена сообщениями перечислены в **области** расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="64029-173">The sample messaging extension is listed in the **Messaging Extensions** pane.</span></span>

1. <span data-ttu-id="64029-174">Выберите **Удаление,** чтобы удалить расширение обмена сообщениями, выберите **Настройка** и выполните те же действия, что и [для ботов.](#bots)</span><span class="sxs-lookup"><span data-stu-id="64029-174">Select **Delete** to remove the messaging extension, select **Set up**, and follow the same steps used for [bots](#bots).</span></span> <span data-ttu-id="64029-175">Отображается **диалоговое окно расширения** обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="64029-175">The **Messaging Extension** dialog box is displayed.</span></span>
1. <span data-ttu-id="64029-176">Выберите **вкладку Использование существующих ботов** **и выберите один из существующих ботов.**</span><span class="sxs-lookup"><span data-stu-id="64029-176">Select the **Use existing bot** tab and **Select from one of my existing bots**.</span></span>
1. <span data-ttu-id="64029-177">Выберите бот, созданный из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="64029-177">Select the bot you created from the drop-down menu.</span></span> <span data-ttu-id="64029-178">Добавьте имя **Бота** и **выберите Сохранить,** чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="64029-178">Add a **Bot name** and select **Save** to close the dialog box.</span></span>
1. <span data-ttu-id="64029-179">В разделе **Команда** выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="64029-179">Under the **Command** section, select **Add**.</span></span> <span data-ttu-id="64029-180">Чтобы добавить команду на основе поиска, выберите разрешить пользователям запрашивать у службы сведения и вставить их **в вариант сообщения.**</span><span class="sxs-lookup"><span data-stu-id="64029-180">To add a search-based command, select the **Allow users to query your service for information and insert that into a message** option.</span></span>
1. <span data-ttu-id="64029-181">В **диалоговом окне** Новая команда введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="64029-181">In the **New command** dialog box, enter the following values:</span></span>

    <span data-ttu-id="64029-182">В **новой команде:**</span><span class="sxs-lookup"><span data-stu-id="64029-182">Under **New command**:</span></span>

    - <span data-ttu-id="64029-183">**Командный ID:** Введите случайный текст</span><span class="sxs-lookup"><span data-stu-id="64029-183">**Command ID**: Enter random text</span></span>
    - <span data-ttu-id="64029-184">**Название:** Введите случайное название</span><span class="sxs-lookup"><span data-stu-id="64029-184">**Title**: Enter random title</span></span>
    - <span data-ttu-id="64029-185">**Описание.** Введите случайное описание</span><span class="sxs-lookup"><span data-stu-id="64029-185">**Description**: Enter random description</span></span>

    <span data-ttu-id="64029-186">В **параметре**:</span><span class="sxs-lookup"><span data-stu-id="64029-186">Under **Parameter**:</span></span>

    - <span data-ttu-id="64029-187">**Имя.** Введите имя параметра</span><span class="sxs-lookup"><span data-stu-id="64029-187">**Name**: Enter the parameter name</span></span>
    - <span data-ttu-id="64029-188">**Название:** Введите название карты</span><span class="sxs-lookup"><span data-stu-id="64029-188">**Title**: Enter the card title</span></span>
    - <span data-ttu-id="64029-189">**Описание.** Введите описание карты</span><span class="sxs-lookup"><span data-stu-id="64029-189">**Description**: Enter card description</span></span>

1. <span data-ttu-id="64029-190">После ввода сведений выберите **Сохранить,** чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="64029-190">After you enter the information, select **Save** to close the dialog box.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="64029-191">Регистрация приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="64029-191">Register your app in Teams</span></span>

<span data-ttu-id="64029-192">После ввода сведений о приложении выполните следующие действия, чтобы зарегистрировать приложение в Teams:</span><span class="sxs-lookup"><span data-stu-id="64029-192">After entering the details of your app, complete the following steps to register your app in Teams:</span></span>

1. <span data-ttu-id="64029-193">Используйте **Test и распространение** App Studio для установки приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="64029-193">Use **Test and distribute** of App Studio to install your app in Teams.</span></span> 
1. <span data-ttu-id="64029-194">Обновите свое хозяйное приложение с помощью ID приложения и пароля для бота.</span><span class="sxs-lookup"><span data-stu-id="64029-194">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="64029-195">Для примера приложения используйте один и тот же код приложения и пароль для расширения бота и обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="64029-195">For the sample app, use the same App ID and password for both bot and messaging extension.</span></span> 
1. <span data-ttu-id="64029-196">Выберите **Тест и раздать** **под Finish** в левой области App Studio:</span><span class="sxs-lookup"><span data-stu-id="64029-196">Select **Test and distribute**  under **Finish** in the left-hand pane of App Studio:</span></span>

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. <span data-ttu-id="64029-197">Чтобы загрузить приложение в Teams, выберите кнопку **Установите** в **статье Test and Distribute:**</span><span class="sxs-lookup"><span data-stu-id="64029-197">To upload your app to Teams, select the **Install** button under **Test and Distribute**:</span></span>

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>
    
    > [!NOTE]
    > <span data-ttu-id="64029-198">Если вы не можете загрузить приложение в сторону, убедитесь, что вы включили [настраиваемую загрузку приложения.](#prepare-your-development-environment)</span><span class="sxs-lookup"><span data-stu-id="64029-198">If you are unable to sideload the app, verify whether you have [enabled custom app uploading](#prepare-your-development-environment).</span></span>

1. <span data-ttu-id="64029-199">Выберите поле **Поиск** в разделе **Добавить в раздел команды** и выберите команду, чтобы добавить пример приложения.</span><span class="sxs-lookup"><span data-stu-id="64029-199">Select the **Search** box in the **Add to a team** section and select a team to add the sample app.</span></span> <span data-ttu-id="64029-200">Вы можете настроить специальную команду для тестирования.</span><span class="sxs-lookup"><span data-stu-id="64029-200">You can set up a special team for testing.</span></span>
1. <span data-ttu-id="64029-201">Выберите **кнопку Установите** в нижней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="64029-201">Select the **Install** button at the bottom of the dialog box.</span></span>

    <span data-ttu-id="64029-202">Ваше приложение теперь доступно в Teams.</span><span class="sxs-lookup"><span data-stu-id="64029-202">Your app is now available in Teams.</span></span> <span data-ttu-id="64029-203">Однако бот и расширение обмена сообщениями не будут работать до тех пор, пока вы не обновите среду хозяйных приложений с помощью кодов и паролей приложения.</span><span class="sxs-lookup"><span data-stu-id="64029-203">However, the bot and the messaging extension will not work until you update the hosted applications environment with the App IDs and passwords.</span></span>

    <img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
