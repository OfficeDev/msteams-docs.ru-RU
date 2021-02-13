### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="e15ba-101">Использование App Studio для обновления пакета приложения</span><span class="sxs-lookup"><span data-stu-id="e15ba-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="e15ba-102">App Studio — это приложение Teams, которое можно установить из магазина Teams.</span><span class="sxs-lookup"><span data-stu-id="e15ba-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="e15ba-103">Это упрощает создание и регистрацию приложения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="e15ba-104">Чтобы установить App Studio в Teams, выберите значок **"Приложения"** в нижней части левой панели и нащите **App Studio.**</span><span class="sxs-lookup"><span data-stu-id="e15ba-104">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**.</span></span>

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

<span data-ttu-id="e15ba-105">Выберите **плитку App Studio** и выберите **"Установить".**</span><span class="sxs-lookup"><span data-stu-id="e15ba-105">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="e15ba-106">Установлена App Studio.</span><span class="sxs-lookup"><span data-stu-id="e15ba-106">The App Studio is installed.</span></span>

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

<span data-ttu-id="e15ba-107">Выберите **вкладку редактора манифеста,** чтобы создать пакет приложения для приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="e15ba-107">Select the **Manifest editor** tab to create the app package for your Teams app.</span></span>

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

<span data-ttu-id="e15ba-108">Пример поставляется с собственным предварительным манифестом и разработан для создания пакета приложения при сборке проекта.</span><span class="sxs-lookup"><span data-stu-id="e15ba-108">The sample comes with its own pre-made manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="e15ba-109">В .NET это делается в Visual Studio, а в Node JS это делается путем ввода в командной строке корневого `gulp` каталога проекта.</span><span class="sxs-lookup"><span data-stu-id="e15ba-109">On .NET this is done in Visual Studio, and on Node JS this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="e15ba-110">Имя сгенерированного пакета приложения **helloworldapp.zip.**</span><span class="sxs-lookup"><span data-stu-id="e15ba-110">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="e15ba-111">Вы можете найти этот файл, если в используемом средстве не ясное расположение.</span><span class="sxs-lookup"><span data-stu-id="e15ba-111">You can search for this file if the location is not clear in the tool you are using.</span></span>

<span data-ttu-id="e15ba-112">Теперь, чтобы изменить этот пакет приложения, выберите **"Импорт существующей** плитки приложения" в **редакторе манифеста.**</span><span class="sxs-lookup"><span data-stu-id="e15ba-112">Now to modify this app package, select the **Import an existing app** tile in the **Manifest editor**.</span></span>

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

<span data-ttu-id="e15ba-113">Щелкните **плитку Hello World** для недавно импортируемого приложения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-113">Click the **Hello World** tile for your newly imported app.</span></span>

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="e15ba-114">На следующем рисунке показан импортируемый пакет приложения в App Studio:</span><span class="sxs-lookup"><span data-stu-id="e15ba-114">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="e15ba-115">В левой части редактора манифеста есть список действий, а справа — список свойств, которые необходимо заполнить для каждого из этих действий.</span><span class="sxs-lookup"><span data-stu-id="e15ba-115">There is a list of steps on the left-hand side of the Manifest editor and on the right-hand side, a list of properties that need to be filled in for each of those steps.</span></span> <span data-ttu-id="e15ba-116">Так как вы начали работу с образцом приложения, большая часть информации уже заполнена. Далее вы сможете изменить части, которые все еще нужно обновить.</span><span class="sxs-lookup"><span data-stu-id="e15ba-116">Since you started with a sample app, much of the information is already filled out. The next steps will walk you through changing the parts that still need to be updated.</span></span>

#### <a name="app-details"></a><span data-ttu-id="e15ba-117">Сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="e15ba-117">App details</span></span>

<span data-ttu-id="e15ba-118">Щелкните запись *сведений о приложении* в области *"Сведения".*</span><span class="sxs-lookup"><span data-stu-id="e15ba-118">Click on the *App details* entry under *Details*.</span></span> <span data-ttu-id="e15ba-119">Нажмите *кнопку* "Создать", чтобы создать новый ид приложения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-119">Click the *Generate* button to create a new app id.</span></span>

<span data-ttu-id="e15ba-120">Ваш новый ид приложения должен выглядеть так: `2322041b-72bf-459d-b107-f4f335bc35bd` .</span><span class="sxs-lookup"><span data-stu-id="e15ba-120">Your new app id should look something like: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="e15ba-121">Ознакомьтесь с остальными сведениями о приложении на правой области и ознакомьтесь с  некоторыми записями, такими как сведения о разработчике и *фирменный брендинг.*</span><span class="sxs-lookup"><span data-stu-id="e15ba-121">Look through the rest of the App details in the right-hand pane, and familiarize yourself with some of the entries such as *Developer information* and *Branding*.</span></span> <span data-ttu-id="e15ba-122">Эти разделы важны при написании нового приложения для распространения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-122">These sections are important if you are writing a new app for distribution.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="e15ba-123">Возможности: вкладки</span><span class="sxs-lookup"><span data-stu-id="e15ba-123">Capabilities: Tabs</span></span>

<span data-ttu-id="e15ba-124">Вкладки — это один из самых простых элементов, добавляемой в приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="e15ba-124">Tabs are among the simplest elements to add to a Teams app.</span></span> <span data-ttu-id="e15ba-125">Пример приложения уже поддерживает несколько вкладок, и их можно включить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e15ba-125">The sample app already supports several tabs, and you can enable them as follows.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="e15ba-126">Вкладка "Группа"</span><span class="sxs-lookup"><span data-stu-id="e15ba-126">Team tab</span></span>

<span data-ttu-id="e15ba-127">В вашем приложении может быть только одна вкладка "Группа".</span><span class="sxs-lookup"><span data-stu-id="e15ba-127">Your app can only have one Team tab.</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="e15ba-128">В этом примере на вкладке "Группа" находится страница конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e15ba-128">In this sample, the Team tab is where your configuration page goes.</span></span> <span data-ttu-id="e15ba-129">Щелкните *символ ...в* конце записи  и выберите "Изменить" в выпадаемом.</span><span class="sxs-lookup"><span data-stu-id="e15ba-129">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="e15ba-130">Измените URL-адрес на то, где следует заменить URL-адрес, используемый выше `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` при размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-130">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="e15ba-131">Личные вкладки</span><span class="sxs-lookup"><span data-stu-id="e15ba-131">Personal tabs</span></span>

<span data-ttu-id="e15ba-132">Ваше приложение может иметь до 16 вкладок, включая вкладку команды.</span><span class="sxs-lookup"><span data-stu-id="e15ba-132">Your app can have up to 16 tabs, including the team tab.</span></span>

<span data-ttu-id="e15ba-133">Личные вкладки представлены иначе, чем на вкладке команды. В списке личных *вкладок должна* быть уже указана вкладка "Hello".</span><span class="sxs-lookup"><span data-stu-id="e15ba-133">Personal tabs are represented differently from the team tab. You should see *Hello Tab* already listed in the personal tabs list.</span></span> <span data-ttu-id="e15ba-134">В настоящее время он имеет значение-замес.. `com.contoso.helloworld.hellotab`</span><span class="sxs-lookup"><span data-stu-id="e15ba-134">At the moment it has a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="e15ba-135">Щелкните *символ ...в* конце записи  и выберите "Изменить" в выпадаемом.</span><span class="sxs-lookup"><span data-stu-id="e15ba-135">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="e15ba-136">Появится следующее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e15ba-136">The following dialog will appear.</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="e15ba-137">Существует два поля, которые необходимо обновить с помощью URL-адреса приложения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-137">There are two fields that you need to update with your app URL.</span></span>

- <span data-ttu-id="e15ba-138">Изменение URL-адреса контента на `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="e15ba-138">Change Content URL to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="e15ba-139">Изменение URL-адреса веб-сайта на `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="e15ba-139">Change Website URL to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="e15ba-140">Где `yourteamsapp.ngrok.io` следует заменить URL-адрес, используемый выше при размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-140">Where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="e15ba-141">Боты</span><span class="sxs-lookup"><span data-stu-id="e15ba-141">Bots</span></span>

<span data-ttu-id="e15ba-142">Боты — это наиболее распространенный способ добавления функций в приложение.</span><span class="sxs-lookup"><span data-stu-id="e15ba-142">Bots are the most common way to add functionality to your app.</span></span> <span data-ttu-id="e15ba-143">В примере hello world уже есть бот в составе примера, но он еще не зарегистрирован в Корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="e15ba-143">The hello world sample already has a bot as part of the sample, but it has not been registered with Microsoft yet.</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="e15ba-144">У бота, импортируемого из примера, еще нет связанного с ним ИД приложения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-144">The bot that was imported from the sample does not have an App ID associated with it yet.</span></span> <span data-ttu-id="e15ba-145">Вам придется создать нового бота, чтобы App Studio мог создать новый ИД приложения и зарегистрировать его в Корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="e15ba-145">You will have to create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span> <span data-ttu-id="e15ba-146">Обратите внимание, что это ИД приложения для бота, который отличается от ИД приложения, созданного для приложения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-146">Note that this is the App ID for the bot, which is different from the App ID created for the app.</span></span> <span data-ttu-id="e15ba-147">Каждому боту в приложении требуется собственный ИД приложения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-147">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="e15ba-148">Нажмите *кнопку удаления* рядом с импортируемым *ботом* в списке ботов.</span><span class="sxs-lookup"><span data-stu-id="e15ba-148">Click the *delete* button next to the *Imported bot* in the bot list.</span></span>

<span data-ttu-id="e15ba-149">Теперь не осталось ботов для показа.</span><span class="sxs-lookup"><span data-stu-id="e15ba-149">Now there are no bots left to show.</span></span> <span data-ttu-id="e15ba-150">Щелкните *"Установка"*.</span><span class="sxs-lookup"><span data-stu-id="e15ba-150">Click *Setup*.</span></span> <span data-ttu-id="e15ba-151">Отобразит *диалоговое окно "Настройка* бота".</span><span class="sxs-lookup"><span data-stu-id="e15ba-151">This will display the *Set up a bot* dialog.</span></span>

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

<span data-ttu-id="e15ba-152">Добавьте имя бота, `Contoso bot` например, и выберите все три кнопки в области.</span><span class="sxs-lookup"><span data-stu-id="e15ba-152">Add a bot name such as `Contoso bot`, and select all three buttons under **Scope**.</span></span>

<span data-ttu-id="e15ba-153">Choose *Create bot* to exit the dialog.</span><span class="sxs-lookup"><span data-stu-id="e15ba-153">Choose *Create bot* to exit the dialog.</span></span> <span data-ttu-id="e15ba-154">App Studio регистрирует бота в корпорации Майкрософт и отображает нового бота в списке ботов.</span><span class="sxs-lookup"><span data-stu-id="e15ba-154">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> <span data-ttu-id="e15ba-155">Пришло бы время открыть текстовый файл в блокноте, скопировать и ввести в него новый бот.</span><span class="sxs-lookup"><span data-stu-id="e15ba-155">Now would be a good time to open a text file in notepad and copy and paste your new bot id into it.</span></span> <span data-ttu-id="e15ba-156">Этот ид потребуется позже.</span><span class="sxs-lookup"><span data-stu-id="e15ba-156">You will need this id later.</span></span>

<span data-ttu-id="e15ba-157">Нажмите *кнопку "Создать* новый пароль" и заметьте пароль в том же текстовом файле, в который вы указали код приложения-бота.</span><span class="sxs-lookup"><span data-stu-id="e15ba-157">Click *Generate New Password*, and make a note of the password in the same text file you noted your Bot app ID in.</span></span> <span data-ttu-id="e15ba-158">Это единственный раз, когда будет показан пароль, поэтому не забудьте сделать это сейчас.</span><span class="sxs-lookup"><span data-stu-id="e15ba-158">This is the only time your password will be shown, so be sure to do this now.</span></span>

<span data-ttu-id="e15ba-159">*Обновите адрес конечной точки бота,* где его следует заменить URL-адресом, который вы использовали при размещении `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` приложения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-159">Update the *Bot endpoint address* to `https://yourteamsapp.ngrok.io/api/messages`, where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

<span data-ttu-id="e15ba-160">Пришло бы время сохранить текстовый файл, если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="e15ba-160">Now would be a good time to save your text file if you have not done so already.</span></span> <span data-ttu-id="e15ba-161">Эти сведения будут добавлены в ваше приложение, которое будет добавлено далее в этом поговом поговом, что обеспечит безопасное взаимодействие с ботом.</span><span class="sxs-lookup"><span data-stu-id="e15ba-161">You will add this information to your hosted app later in this walkthrough, which will allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="e15ba-162">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="e15ba-162">Messaging extensions</span></span>

<span data-ttu-id="e15ba-163">Расширения обмена сообщениями позволяет пользователям запросить сведения из вашей службы и опубликовать эти сведения в виде карточек прямо в беседе канала.</span><span class="sxs-lookup"><span data-stu-id="e15ba-163">Messaging extensions let users ask for information from your service and post that information, in the form of cards, right into the channel conversation.</span></span> <span data-ttu-id="e15ba-164">Расширения сообщений отображаются в нижней части окна составить.</span><span class="sxs-lookup"><span data-stu-id="e15ba-164">Messaging extensions appear along the bottom of the compose box.</span></span>

<span data-ttu-id="e15ba-165">Выберите **расширения сообщений в** области **"Возможности"** в левом столбце App Studio, чтобы настроить расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e15ba-165">Select **Messaging extensions** under **Capabilities** in the left-hand column of App Studio to configure the messaging extension.</span></span>

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

<span data-ttu-id="e15ba-166">Пример расширения обмена сообщениями находится в правой области в **списке расширений обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="e15ba-166">The sample messaging extension is listed in the right-hand pane under **Messaging Extensions**.</span></span> <span data-ttu-id="e15ba-167">Еще **раз нажмите** кнопку "Удалить", чтобы удалить эту запись, а затем нажмите кнопку "Настроить", выполив те же действия, что и для ботов. </span><span class="sxs-lookup"><span data-stu-id="e15ba-167">Select **Delete** again to remove this entry, and then click the *Set up* button following the same steps as you followed for bots.</span></span> <span data-ttu-id="e15ba-168">Отобразит *диалоговое окно расширения* обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e15ba-168">This will display the *Messaging Extension* dialog.</span></span>

<span data-ttu-id="e15ba-169">Выберите *вкладку "Использовать существующий бот",* а затем выберите один *из существующих ботов.*</span><span class="sxs-lookup"><span data-stu-id="e15ba-169">Select the *Use existing bot* tab, then *Select from one of my existing bots*.</span></span> <span data-ttu-id="e15ba-170">В выпадаемом меню выберите бота, созданного в разделе выше.</span><span class="sxs-lookup"><span data-stu-id="e15ba-170">In the drop-down menu, select the bot you created in the section above.</span></span> <span data-ttu-id="e15ba-171">Добавьте имя *бота и* нажмите *кнопку* "Сохранить", чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e15ba-171">Add a *Bot name* and click *Save* to close the dialog.</span></span>

<span data-ttu-id="e15ba-172">В разделе *"Команда"* нажмите кнопку *"Добавить".*</span><span class="sxs-lookup"><span data-stu-id="e15ba-172">Under the *Command* section, click *Add*.</span></span> <span data-ttu-id="e15ba-173">Мы добавляем команду на основе поиска, поэтому выберите параметр *"Разрешить пользователям запрашивать вашу службу...".*</span><span class="sxs-lookup"><span data-stu-id="e15ba-173">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span></span>

<span data-ttu-id="e15ba-174">В **диалоговом окте** "Новая команда" введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-174">In the **New command** dialog, enter the following values.</span></span>

<span data-ttu-id="e15ba-175">В *области "Новая команда" :*</span><span class="sxs-lookup"><span data-stu-id="e15ba-175">Under *New command*:</span></span>

- <span data-ttu-id="e15ba-176">*ИД команды*  = getRandomText</span><span class="sxs-lookup"><span data-stu-id="e15ba-176">*Command ID*  = getRandomText</span></span>
- <span data-ttu-id="e15ba-177">*Title*       = Get some random text for fun</span><span class="sxs-lookup"><span data-stu-id="e15ba-177">*Title*       = Get some random text for fun</span></span>
- <span data-ttu-id="e15ba-178">*Description* = Получает произвольный текст и изображения</span><span class="sxs-lookup"><span data-stu-id="e15ba-178">*Description* = Gets some random text and images</span></span>

<span data-ttu-id="e15ba-179">Under *Parameter*:</span><span class="sxs-lookup"><span data-stu-id="e15ba-179">Under *Parameter*:</span></span>

- <span data-ttu-id="e15ba-180">*Name*        = cardTitle</span><span class="sxs-lookup"><span data-stu-id="e15ba-180">*Name*        = cardTitle</span></span>
- <span data-ttu-id="e15ba-181">*Title*       = Card title</span><span class="sxs-lookup"><span data-stu-id="e15ba-181">*Title*       = Card title</span></span>
- <span data-ttu-id="e15ba-182">*Description* = Card title to use</span><span class="sxs-lookup"><span data-stu-id="e15ba-182">*Description* = Card title to use</span></span>

<span data-ttu-id="e15ba-183">После того как вы ввели данные, нажмите кнопку *"Сохранить",* чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e15ba-183">Once you're entered the information, click *Save* to close the dialog.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="e15ba-184">Регистрация приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="e15ba-184">Register your app in Teams</span></span>

<span data-ttu-id="e15ba-185">Теперь вы завершили ввод сведений о своем приложении, но осталось два следующих этапа:</span><span class="sxs-lookup"><span data-stu-id="e15ba-185">You have now completed entering the details of your app, but the following two steps remain:</span></span>
1. <span data-ttu-id="e15ba-186">Используйте раздел "Тестирование и распространение" в App Studio, чтобы установить приложение в Teams.</span><span class="sxs-lookup"><span data-stu-id="e15ba-186">Use the Test and Distribute section of App Studio to install your app in Teams.</span></span>
1. <span data-ttu-id="e15ba-187">Обновите свое приложение с помощью ИД приложения и пароля для бота.</span><span class="sxs-lookup"><span data-stu-id="e15ba-187">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="e15ba-188">Помните, что в примере предполагается использовать один и тот же код приложения и пароль для бота и расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e15ba-188">Remember that the sample expects to use the same App ID and password for both the bot and the messaging extension.</span></span>

<span data-ttu-id="e15ba-189">Выберите элемент **"Тестирование и распространение"** в области **"Готово"** в левом столбце App Studio.</span><span class="sxs-lookup"><span data-stu-id="e15ba-189">Select the **Test and distribute** item under **Finish** in the left-hand column of App Studio.</span></span>

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

<span data-ttu-id="e15ba-190">Чтобы отправить приложение в Teams, нажмите кнопку *"Установить"* в области *"Тестирование и распространение".*</span><span class="sxs-lookup"><span data-stu-id="e15ba-190">In order to upload your app to Teams, click the *Install* button under *Test and Distribute*.</span></span>

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

<span data-ttu-id="e15ba-191">Выберите поле **поиска** в разделе **"Добавить в** команду" и выберите команду для добавления примера приложения.</span><span class="sxs-lookup"><span data-stu-id="e15ba-191">Select the **Search** box in the **Add to a team** section and select a team to add the sample app to.</span></span> <span data-ttu-id="e15ba-192">Обычно можно настроить специальную команду для тестирования.</span><span class="sxs-lookup"><span data-stu-id="e15ba-192">Usually, you can set up a special team for testing.</span></span>

<span data-ttu-id="e15ba-193">Выберите **кнопку "Установить"** в нижней части диалога.</span><span class="sxs-lookup"><span data-stu-id="e15ba-193">Select the **Install** button at the bottom of the dialog.</span></span>

<span data-ttu-id="e15ba-194">Это завершает часть Этого по walkthrough в App Studio.</span><span class="sxs-lookup"><span data-stu-id="e15ba-194">This finishes the App Studio portion of this walkthrough.</span></span> <span data-ttu-id="e15ba-195">Теперь приложение должно работать в Teams, но бот и расширение обмена сообщениями не будут работать, пока вы не обновите среду приложений, чтобы узнать, что такое коды и пароли приложений.</span><span class="sxs-lookup"><span data-stu-id="e15ba-195">You should now see your app running in Teams, however, the bot and the messaging extension will not work until you update the hosted applications environment to know what the App IDs and passwords are.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
