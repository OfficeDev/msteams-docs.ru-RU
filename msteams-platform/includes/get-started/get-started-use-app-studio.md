### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="591c4-101">Используйте App Studio для обновления пакета приложений</span><span class="sxs-lookup"><span data-stu-id="591c4-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="591c4-102">App Studio — это Teams приложение, которое можно установить из Teams магазина.</span><span class="sxs-lookup"><span data-stu-id="591c4-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="591c4-103">Это упрощает создание и регистрацию приложения.</span><span class="sxs-lookup"><span data-stu-id="591c4-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="591c4-104">Выполните следующие действия по обновлению пакета приложений:</span><span class="sxs-lookup"><span data-stu-id="591c4-104">Complete the following steps to update the app package:</span></span>

1. <span data-ttu-id="591c4-105">Чтобы установить App Studio в Teams, выберите значок **Apps** в нижней части левой панели и выберите **App Studio:**</span><span class="sxs-lookup"><span data-stu-id="591c4-105">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**:</span></span>

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. <span data-ttu-id="591c4-106">Выберите **плитку App Studio** и **установите**.</span><span class="sxs-lookup"><span data-stu-id="591c4-106">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="591c4-107">Установлена App Studio:</span><span class="sxs-lookup"><span data-stu-id="591c4-107">The App Studio is installed:</span></span>

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. <span data-ttu-id="591c4-108">Чтобы создать пакет приложений для Teams, выберите вкладку **Редактор Манифеста** в **App Studio:**</span><span class="sxs-lookup"><span data-stu-id="591c4-108">To create the app package for your Teams app, select the **Manifest editor** tab in **App Studio**:</span></span>

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    <span data-ttu-id="591c4-109">Пример поставляется с собственным манифестом и предназначен для создания пакета приложений при построении проекта.</span><span class="sxs-lookup"><span data-stu-id="591c4-109">The sample comes with its own manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="591c4-110">В .NET это делается в Visual Studio и Node.js это делается путем ввода в командной строке в корневом `gulp` каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="591c4-110">On .NET this is done in Visual Studio and on Node.js this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

    <span data-ttu-id="591c4-111">Имя сгенерированного пакета приложений **helloworldapp.zip**.</span><span class="sxs-lookup"><span data-stu-id="591c4-111">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="591c4-112">Этот файл можно искать, если в используемом средстве расположение не ясно.</span><span class="sxs-lookup"><span data-stu-id="591c4-112">You can search for this file if the location is not clear in the tool you are using.</span></span>

1. <span data-ttu-id="591c4-113">Чтобы изменить этот пакет приложений, выберите **импорт существующего** приложения в **редакторе Manifest:**</span><span class="sxs-lookup"><span data-stu-id="591c4-113">Now to modify this app package, select **Import an existing app** in the **Manifest editor**:</span></span>

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. <span data-ttu-id="591c4-114">Выберите **плитку Hello World** для вашего недавно импортируемого приложения:</span><span class="sxs-lookup"><span data-stu-id="591c4-114">Select the **Hello World** tile for your newly imported app:</span></span>

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="591c4-115">На следующем изображении показан импортируемый пакет приложений в App Studio:</span><span class="sxs-lookup"><span data-stu-id="591c4-115">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="591c4-116">На левой стороне редактора Манифеста находится список действий.</span><span class="sxs-lookup"><span data-stu-id="591c4-116">On the left-hand side of the Manifest editor there is a list of steps.</span></span> <span data-ttu-id="591c4-117">В правой части имеется список свойств, которые необходимо заполнить для каждого шага.</span><span class="sxs-lookup"><span data-stu-id="591c4-117">On the right-hand side there is a list of properties that need to be filled in for each step.</span></span> <span data-ttu-id="591c4-118">По мере начала работы с примерным приложением большая часть сведений уже завершена.</span><span class="sxs-lookup"><span data-stu-id="591c4-118">As you started with a sample app, much of the information is already completed.</span></span> <span data-ttu-id="591c4-119">Следующие действия позволяют обновить свойства приложения Hello World.</span><span class="sxs-lookup"><span data-stu-id="591c4-119">The next steps enable you to update the properties of the Hello World app.</span></span>

#### <a name="app-details"></a><span data-ttu-id="591c4-120">Сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="591c4-120">App details</span></span>

<span data-ttu-id="591c4-121">Выберите **сведения о приложении** в **статье Details**.</span><span class="sxs-lookup"><span data-stu-id="591c4-121">Select **App details** under **Details**.</span></span> <span data-ttu-id="591c4-122">Выберите **кнопку Создать,** чтобы создать новый ID приложения.</span><span class="sxs-lookup"><span data-stu-id="591c4-122">Select the **Generate** button to create a new App ID.</span></span>

<span data-ttu-id="591c4-123">Ваш новый ID приложения похож на `2322041b-72bf-459d-b107-f4f335bc35bd` .</span><span class="sxs-lookup"><span data-stu-id="591c4-123">Your new App ID is similar to `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="591c4-124">Сведения о приложении в правой области, включая сведения **разработчика** и **сведения о брендинге.**</span><span class="sxs-lookup"><span data-stu-id="591c4-124">Go through the app details in the right-hand pane including **Developer information** and **Branding** details.</span></span> <span data-ttu-id="591c4-125">Эти сведения важны, если вы пишете новое приложение для распространения.</span><span class="sxs-lookup"><span data-stu-id="591c4-125">These details are important if you are writing a new app for distribution.</span></span>

#### <a name="tabs"></a><span data-ttu-id="591c4-126">Вкладки</span><span class="sxs-lookup"><span data-stu-id="591c4-126">Tabs</span></span>

<span data-ttu-id="591c4-127">Просто добавить вкладки в приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="591c4-127">It is simple to add tabs to a Teams app.</span></span> <span data-ttu-id="591c4-128">Пример приложения уже поддерживает несколько вкладок, и вы можете включить их.</span><span class="sxs-lookup"><span data-stu-id="591c4-128">The sample app already supports several tabs, and you can enable them.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="591c4-129">Вкладка Team</span><span class="sxs-lookup"><span data-stu-id="591c4-129">Team tab</span></span>

<span data-ttu-id="591c4-130">В приложении может быть только одна вкладка Team:</span><span class="sxs-lookup"><span data-stu-id="591c4-130">Your app can only have one Team tab:</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="591c4-131">В этом примере вкладка Team отображает страницу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="591c4-131">In this sample, the Team tab is where your configuration page is displayed.</span></span> <span data-ttu-id="591c4-132">Выберите **символ url-адреса** конфигурации **Tab** и выберите **Изменить** из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="591c4-132">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="591c4-133">Измените URL-адрес на то, где необходимо заменить URL-адрес, используемый при `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` [размещении приложения.](#host-the-sample-app)</span><span class="sxs-lookup"><span data-stu-id="591c4-133">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` must be replaced with the URL that you used when [hosting your app](#host-the-sample-app).</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="591c4-134">Личные вкладки</span><span class="sxs-lookup"><span data-stu-id="591c4-134">Personal tabs</span></span>

<span data-ttu-id="591c4-135">В вашем приложении может быть до 16 вкладок, включая вкладку Team.</span><span class="sxs-lookup"><span data-stu-id="591c4-135">Your app can have up to 16 tabs, including the Team tab.</span></span>

<span data-ttu-id="591c4-136">Личные вкладки отличаются от вкладки **Team. Вкладка Hello уже** указана в списке личных вкладок со значением места. `com.contoso.helloworld.hellotab`</span><span class="sxs-lookup"><span data-stu-id="591c4-136">Personal tabs are different from the Team tab. **Hello Tab** is already listed in the personal tabs list with a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="591c4-137">Выберите **символ url-адреса** конфигурации **Tab** и выберите **Изменить** из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="591c4-137">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="591c4-138">Появится следующее диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="591c4-138">The following dialog box appears:</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="591c4-139">Обновление следующих полей с URL-адресом приложения:</span><span class="sxs-lookup"><span data-stu-id="591c4-139">Update the following boxes with your app URL:</span></span>

- <span data-ttu-id="591c4-140">Измените **поле URL-адреса контента** на `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="591c4-140">Change the **Content URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="591c4-141">Изменение **URL-адреса веб-сайта** на `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="591c4-141">Change the **Website URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="591c4-142">Замените `yourteamsapp.ngrok.io` URL-адрес, используемый при размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="591c4-142">Replace `yourteamsapp.ngrok.io` by the URL that you used when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="591c4-143">Боты</span><span class="sxs-lookup"><span data-stu-id="591c4-143">Bots</span></span>

<span data-ttu-id="591c4-144">Легко добавить функции ботов в приложение.</span><span class="sxs-lookup"><span data-stu-id="591c4-144">It is easy to add the bots functionality to your app.</span></span> <span data-ttu-id="591c4-145">В **примере Приложения Hello World** уже есть бот в качестве части примера, но его необходимо зарегистрировать в Корпорации Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="591c4-145">The **Hello World** sample app already has a bot as part of the sample, but you must register it with Microsoft:</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="591c4-146">У бота, импортируемого из примера, нет связанного СД приложения.</span><span class="sxs-lookup"><span data-stu-id="591c4-146">The bot that was imported from the sample does not have an associated App ID.</span></span> <span data-ttu-id="591c4-147">Необходимо создать новый бот, чтобы App Studio создал новый ID приложения и зарегистрировал его в Корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="591c4-147">You must create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span>

> [!NOTE]
> <span data-ttu-id="591c4-148">ID приложения, созданный App Studio для бота, отличается от ID приложения, созданного для приложения.</span><span class="sxs-lookup"><span data-stu-id="591c4-148">The App ID created by App Studio for the bot is different from the App ID created for the app.</span></span> <span data-ttu-id="591c4-149">Каждому боту в приложении требуется свой собственный ID приложения.</span><span class="sxs-lookup"><span data-stu-id="591c4-149">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="591c4-150">Выполните следующие действия по настройке бота:</span><span class="sxs-lookup"><span data-stu-id="591c4-150">Complete the following steps to setup your bot:</span></span>

1. <span data-ttu-id="591c4-151">Выберите **Удаление** рядом с импортируемым ботом в списке ботов.</span><span class="sxs-lookup"><span data-stu-id="591c4-151">Select **Delete** next to the imported bot in the bot list.</span></span> <span data-ttu-id="591c4-152">Теперь для показа не осталось ботов.</span><span class="sxs-lookup"><span data-stu-id="591c4-152">Now there are no bots left to show.</span></span> 
1. <span data-ttu-id="591c4-153">Выберите **Установку,** чтобы **отобразить диалоговое** окно "Настройка бота".</span><span class="sxs-lookup"><span data-stu-id="591c4-153">Select **Setup** to display the **Set up a bot** dialog box.</span></span>

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. <span data-ttu-id="591c4-154">Добавьте бот с именем **бота Contoso** и выберите все три флажка в **области.**</span><span class="sxs-lookup"><span data-stu-id="591c4-154">Add a bot name **Contoso bot** and select all three check boxes under **Scope**.</span></span>
1. <span data-ttu-id="591c4-155">Выберите **Сохранить,** чтобы выйти из диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="591c4-155">Choose **Save** to exit the dialog box.</span></span> <span data-ttu-id="591c4-156">App Studio регистрирует бот в Microsoft и отображает новый бот в списке ботов.</span><span class="sxs-lookup"><span data-stu-id="591c4-156">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> 
1. <span data-ttu-id="591c4-157">Теперь откройте текстовый файл в блокноте и скопируйте и вклейте в него новый бот-ИД.</span><span class="sxs-lookup"><span data-stu-id="591c4-157">Now open a text file in notepad and copy and paste your new bot ID into it.</span></span>
1. <span data-ttu-id="591c4-158">Нажмите **кнопку Создание нового пароля** и обратите внимание на пароль в том же текстовом файле, который вы отметили в коде бота App.</span><span class="sxs-lookup"><span data-stu-id="591c4-158">Click **Generate New Password**, and note the password in the same text file you noted your bot App ID.</span></span>
1. <span data-ttu-id="591c4-159">**Обновите адрес конечной точки Bot** и замените URL-адресом, используемым при `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="591c4-159">Update the **Bot endpoint address** to `https://yourteamsapp.ngrok.io/api/messages`, and replace `yourteamsapp.ngrok.io` with the URL that you used when hosting your app.</span></span>
1. <span data-ttu-id="591c4-160">Теперь сохраните текстовый файл, так как вы должны добавить сведения из файла в ваше хост-приложение, чтобы обеспечить безопасное общение с ботом.</span><span class="sxs-lookup"><span data-stu-id="591c4-160">Now save your text file as you must add the information from the file to your hosted app to allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="591c4-161">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="591c4-161">Messaging extensions</span></span>

<span data-ttu-id="591c4-162">Расширения обмена сообщениями позволяет пользователям запросить сведения из вашей службы и опубликовать эти сведения.</span><span class="sxs-lookup"><span data-stu-id="591c4-162">Messaging extensions let users ask for information from your service and post that information.</span></span> <span data-ttu-id="591c4-163">Сведения вывешиты в виде карточек в диалог канала.</span><span class="sxs-lookup"><span data-stu-id="591c4-163">The information is posted in the form of cards into the channel conversation.</span></span> <span data-ttu-id="591c4-164">Расширения обмена сообщениями отображаются в нижней части окна составить.</span><span class="sxs-lookup"><span data-stu-id="591c4-164">Messaging extensions appear at the bottom of the compose box.</span></span>

<span data-ttu-id="591c4-165">Выполните следующие действия по настройке расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="591c4-165">Complete the following steps to setup your messaging extension:</span></span>

1. <span data-ttu-id="591c4-166">Выберите **расширения обмена сообщениями** в соответствии с **возможностями** в левом окантовке App Studio для настройки расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="591c4-166">Select **Messaging extensions** under **Capabilities** in the left-hand pane of App Studio to configure the messaging extension:</span></span>

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    <span data-ttu-id="591c4-167">Расширение примера обмена сообщениями перечислены в **области** расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="591c4-167">The sample messaging extension is listed in the **Messaging Extensions** pane.</span></span>

1. <span data-ttu-id="591c4-168">Выберите **Удаление,** чтобы удалить расширение обмена сообщениями, выберите **Настройка** и выполните те же действия, что и [для ботов.](#bots)</span><span class="sxs-lookup"><span data-stu-id="591c4-168">Select **Delete** to remove the messaging extension, select **Set up**, and follow the same steps used for [bots](#bots).</span></span> <span data-ttu-id="591c4-169">Отображается **диалоговое окно расширения** обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="591c4-169">The **Messaging Extension** dialog box is displayed.</span></span>
1. <span data-ttu-id="591c4-170">Выберите **вкладку Использование существующих ботов** **и выберите один из существующих ботов.**</span><span class="sxs-lookup"><span data-stu-id="591c4-170">Select the **Use existing bot** tab and **Select from one of my existing bots**.</span></span>
1. <span data-ttu-id="591c4-171">Выберите бот, созданный из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="591c4-171">Select the bot you created from the drop-down menu.</span></span> <span data-ttu-id="591c4-172">Добавьте имя **Бота** и **выберите Сохранить,** чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="591c4-172">Add a **Bot name** and select **Save** to close the dialog box.</span></span>
1. <span data-ttu-id="591c4-173">В разделе **Команда** выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="591c4-173">Under the **Command** section, select **Add**.</span></span> <span data-ttu-id="591c4-174">Чтобы добавить команду на основе поиска, выберите разрешить пользователям запрашивать у службы сведения и вставить их **в вариант сообщения.**</span><span class="sxs-lookup"><span data-stu-id="591c4-174">To add a search-based command, select the **Allow users to query your service for information and insert that into a message** option.</span></span>
1. <span data-ttu-id="591c4-175">В **диалоговом окне** Новая команда введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="591c4-175">In the **New command** dialog box, enter the following values:</span></span>

    <span data-ttu-id="591c4-176">В **новой команде:**</span><span class="sxs-lookup"><span data-stu-id="591c4-176">Under **New command**:</span></span>

    - <span data-ttu-id="591c4-177">**Командный ID:** Введите случайный текст</span><span class="sxs-lookup"><span data-stu-id="591c4-177">**Command ID**: Enter random text</span></span>
    - <span data-ttu-id="591c4-178">**Название:** Введите случайное название</span><span class="sxs-lookup"><span data-stu-id="591c4-178">**Title**: Enter random title</span></span>
    - <span data-ttu-id="591c4-179">**Описание.** Введите случайное описание</span><span class="sxs-lookup"><span data-stu-id="591c4-179">**Description**: Enter random description</span></span>

    <span data-ttu-id="591c4-180">В **параметре**:</span><span class="sxs-lookup"><span data-stu-id="591c4-180">Under **Parameter**:</span></span>

    - <span data-ttu-id="591c4-181">**Имя.** Введите имя параметра</span><span class="sxs-lookup"><span data-stu-id="591c4-181">**Name**: Enter the parameter name</span></span>
    - <span data-ttu-id="591c4-182">**Название:** Введите название карты</span><span class="sxs-lookup"><span data-stu-id="591c4-182">**Title**: Enter the card title</span></span>
    - <span data-ttu-id="591c4-183">**Описание.** Введите описание карты</span><span class="sxs-lookup"><span data-stu-id="591c4-183">**Description**: Enter card description</span></span>

1. <span data-ttu-id="591c4-184">После ввода сведений выберите **Сохранить,** чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="591c4-184">After you enter the information, select **Save** to close the dialog box.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="591c4-185">Регистрация приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="591c4-185">Register your app in Teams</span></span>

<span data-ttu-id="591c4-186">После ввода сведений о приложении выполните следующие действия, чтобы зарегистрировать приложение в Teams:</span><span class="sxs-lookup"><span data-stu-id="591c4-186">After entering the details of your app, complete the following steps to register your app in Teams:</span></span>

1. <span data-ttu-id="591c4-187">Используйте **Test и распространение** App Studio для установки приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="591c4-187">Use **Test and distribute** of App Studio to install your app in Teams.</span></span> 
1. <span data-ttu-id="591c4-188">Обновите свое хозяйное приложение с помощью ID приложения и пароля для бота.</span><span class="sxs-lookup"><span data-stu-id="591c4-188">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="591c4-189">Для примера приложения используйте один и тот же код приложения и пароль для расширения бота и обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="591c4-189">For the sample app, use the same App ID and password for both bot and messaging extension.</span></span> 
1. <span data-ttu-id="591c4-190">Выберите **Тест и раздать** **под Finish** в левой области App Studio:</span><span class="sxs-lookup"><span data-stu-id="591c4-190">Select **Test and distribute**  under **Finish** in the left-hand pane of App Studio:</span></span>

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. <span data-ttu-id="591c4-191">Чтобы загрузить приложение в Teams, выберите кнопку **Установите** в **статье Test and Distribute:**</span><span class="sxs-lookup"><span data-stu-id="591c4-191">To upload your app to Teams, select the **Install** button under **Test and Distribute**:</span></span>

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

1. <span data-ttu-id="591c4-192">Выберите поле **Поиск** в разделе **Добавить в раздел команды** и выберите команду, чтобы добавить пример приложения.</span><span class="sxs-lookup"><span data-stu-id="591c4-192">Select the **Search** box in the **Add to a team** section and select a team to add the sample app.</span></span> <span data-ttu-id="591c4-193">Вы можете настроить специальную команду для тестирования.</span><span class="sxs-lookup"><span data-stu-id="591c4-193">You can set up a special team for testing.</span></span>
1. <span data-ttu-id="591c4-194">Выберите **кнопку Установите** в нижней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="591c4-194">Select the **Install** button at the bottom of the dialog box.</span></span>

<span data-ttu-id="591c4-195">Ваше приложение теперь доступно в Teams.</span><span class="sxs-lookup"><span data-stu-id="591c4-195">Your app is now available in Teams.</span></span> <span data-ttu-id="591c4-196">Однако бот и расширение обмена сообщениями не будут работать до тех пор, пока вы не обновите среду хозяйных приложений с помощью кодов и паролей приложения.</span><span class="sxs-lookup"><span data-stu-id="591c4-196">However, the bot and the messaging extension will not work until you update the hosted applications environment with the App IDs and passwords.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
