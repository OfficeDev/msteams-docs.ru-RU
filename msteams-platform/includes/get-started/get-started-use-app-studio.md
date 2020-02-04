### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="faefa-101">Обновление пакета приложения с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="faefa-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="faefa-102">App Studio — это приложение Teams, которое можно установить из хранилища Teams.</span><span class="sxs-lookup"><span data-stu-id="faefa-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="faefa-103">Он упрощает создание и регистрацию приложения.</span><span class="sxs-lookup"><span data-stu-id="faefa-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="faefa-104">Чтобы установить приложение App Studio в Teams, щелкните значок магазин приложений в нижней части левой панели и найдите приложение App Studio.</span><span class="sxs-lookup"><span data-stu-id="faefa-104">To install App Studio in Teams, click on the app store icon at the bottom of the left hand bar, and search for App Studio.</span></span>

<img  width="450px" title="Поиск App Studio в магазине" src="~/assets/images/get-started/app-studio-store.png"/>

<span data-ttu-id="faefa-106">Найдя плитку для App Studio, щелкните ее и выберите пункт *установить* в появившемся диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="faefa-106">Once you find the tile for App Studio, click on it and choose *install* in the dialog that pops up.</span></span>

<img  width="450px" title="Установка App Studio" src="~/assets/images/get-started/app-studio-install.png"/>

<span data-ttu-id="faefa-108">После установки App Studio щелкните вкладку редактор манифеста, чтобы приступить к созданию пакета приложения для приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="faefa-108">Once App Studio is installed click on the Manifest editor tab to begin creating the app package for your Teams app.</span></span>

<img  width="450px" title="App Studio" src="~/assets/images/get-started/app-studio.png"/>

<span data-ttu-id="faefa-110">Пример сопровождается собственным манифестом и предназначен для создания пакета приложения при построении проекта.</span><span class="sxs-lookup"><span data-stu-id="faefa-110">The sample comes with its own pre-made manifest, and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="faefa-111">В .NET это делается в Visual Studio, а на узле JS это делается путем ввода `gulp` в командной строке корневого каталога проекта.</span><span class="sxs-lookup"><span data-stu-id="faefa-111">On .NET this is done in Visual Studio, and on Node JS this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="faefa-112">Имя созданного пакета приложения — *хелловорлдапп. zip*.</span><span class="sxs-lookup"><span data-stu-id="faefa-112">The name of the generated app package is *helloworldapp.zip*.</span></span> <span data-ttu-id="faefa-113">Вы можете выполнить поиск этого файла, если расположение не было ясно в используемом средстве.</span><span class="sxs-lookup"><span data-stu-id="faefa-113">You can search for this file if the location is not clear in the tool you are using.</span></span>

<span data-ttu-id="faefa-114">В следующей части пошагового руководства вы собираетесь изменить этот пакет приложения, выбрав в редакторе манифеста *Импорт имеющейся плитки приложения* .</span><span class="sxs-lookup"><span data-stu-id="faefa-114">In the next part of this walkthrough you are going to modify this app package by selecting the *Import an existing app* tile in the Manifest Editor.</span></span>

<img  width="450px" title="Импорт приложения" src="~/assets/images/get-started/app-studio-import.png"/>

<span data-ttu-id="faefa-116">После импорта пакета приложений приложение Studio Studio должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="faefa-116">Once the app package has been imported App Studio should look like this:</span></span>

<img  width="450px" title="Импорт приложения" src="~/assets/images/get-started/app-studio-imported-app.png"/>

<span data-ttu-id="faefa-118">Щелкните плитку для нового импортированного приложения *Hello World*.</span><span class="sxs-lookup"><span data-stu-id="faefa-118">Click on the tile for your newly imported app, *Hello World*.</span></span>

<img  width="450px" title="Импорт приложения" src="~/assets/images/get-started/app-studio-manifest-editor.png"/>

<span data-ttu-id="faefa-120">В левой части редактора манифеста есть список шагов, а в правом списке свойств, которые необходимо заполнить для каждого из этих шагов.</span><span class="sxs-lookup"><span data-stu-id="faefa-120">There is a list of steps in the left-hand side of the Manifest editor, and on the right a list of properties that need to be filled in for each of those steps.</span></span> <span data-ttu-id="faefa-121">С момента начала работы с примером приложения многие сведения уже заполнены. Дальнейшие действия помогут изменить те части, которые все еще нуждаются в обновлении.</span><span class="sxs-lookup"><span data-stu-id="faefa-121">Since you started with a sample app, much of the information is already filled out. The next steps will walk you through changing the parts that still need to be updated.</span></span>

#### <a name="app-details"></a><span data-ttu-id="faefa-122">Сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="faefa-122">App details</span></span>

<span data-ttu-id="faefa-123">В разделе *Details*(сведения о приложении) щелкните запись *сведения о приложении* .</span><span class="sxs-lookup"><span data-stu-id="faefa-123">Click on the *App details* entry under *Details*.</span></span> <span data-ttu-id="faefa-124">Нажмите кнопку *создать* , чтобы создать новый идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="faefa-124">Click the *Generate* button to create a new app id.</span></span>

<span data-ttu-id="faefa-125">Новый идентификатор приложения должен выглядеть примерно так: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span><span class="sxs-lookup"><span data-stu-id="faefa-125">Your new app id should look something like: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="faefa-126">Просмотрите остальные сведения о приложении в правой области и ознакомьтесь с некоторыми из таких записей, как *сведения об авторе* и *фирменная символика*.</span><span class="sxs-lookup"><span data-stu-id="faefa-126">Look through the rest of the App details in the right hand pane, and familiarize yourself with some of the entries such as *Developer information* and *Branding*.</span></span> <span data-ttu-id="faefa-127">Эти разделы важны, если вы пишете новое приложение для распространения.</span><span class="sxs-lookup"><span data-stu-id="faefa-127">These sections are important if you are writing a new app for distribution.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="faefa-128">Возможности: вкладки</span><span class="sxs-lookup"><span data-stu-id="faefa-128">Capabilities: Tabs</span></span>

<span data-ttu-id="faefa-129">Вкладки находятся среди самых простых элементов, добавляемых в приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="faefa-129">Tabs are among the simplest elements to add to a Teams app.</span></span> <span data-ttu-id="faefa-130">Пример приложения уже поддерживает несколько вкладок, и вы можете включить их следующим образом.</span><span class="sxs-lookup"><span data-stu-id="faefa-130">The sample app already supports several tabs, and you can enable them as follows.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="faefa-131">Вкладка "Группа"</span><span class="sxs-lookup"><span data-stu-id="faefa-131">Team tab</span></span>

<span data-ttu-id="faefa-132">Ваше приложение может иметь только одну вкладку группы.</span><span class="sxs-lookup"><span data-stu-id="faefa-132">Your app can only have one Team tab.</span></span>

<img  width="450px" title="Добавление вкладки "команды"" src="~/assets/images/get-started/app-studio-manifest-editor-tabs.png"/>

<span data-ttu-id="faefa-134">В этом примере на вкладке Группа размещается страница настройки.</span><span class="sxs-lookup"><span data-stu-id="faefa-134">In this sample, the Team tab is where your configuration page goes.</span></span> <span data-ttu-id="faefa-135">Щелкните символ *..* . в конце записи и выберите команду *изменить* в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="faefa-135">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="faefa-136">Измените URL-адрес `https://yourteamsapp.ngrok.io/configure` , `yourteamsapp.ngrok.io` на который следует заменить URL-адрес, который использовался при размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="faefa-136">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="faefa-137">Личные вкладки</span><span class="sxs-lookup"><span data-stu-id="faefa-137">Personal tabs</span></span>

<span data-ttu-id="faefa-138">Ваше приложение может иметь до 16 вкладок, в том числе вкладку "Группа".</span><span class="sxs-lookup"><span data-stu-id="faefa-138">Your app can have up to 16 tabs, including the team tab.</span></span>

<span data-ttu-id="faefa-139">Личные вкладки представлены по-разному на вкладке Группа. *Вкладка Привет* должна отображаться в списке личные вкладки.</span><span class="sxs-lookup"><span data-stu-id="faefa-139">Personal tabs are represented differently from the team tab. You should see *Hello Tab* already listed in the personal tabs list.</span></span> <span data-ttu-id="faefa-140">В данный момент он имеет значение `com.contoso.helloworld.hellotab`заполнителя.</span><span class="sxs-lookup"><span data-stu-id="faefa-140">At the moment it has a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="faefa-141">Щелкните символ *..* . в конце записи и выберите команду *изменить* в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="faefa-141">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="faefa-142">Появится следующее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="faefa-142">The following dialog will appear.</span></span>

<img  width="450px" title="Добавление диалогового окна личных вкладок" src="~/assets/images/get-started/app-studio-manifest-editor-p-tabs-dialog.png"/>

<span data-ttu-id="faefa-144">Существует два поля, которые необходимо обновить с помощью URL-адреса приложения.</span><span class="sxs-lookup"><span data-stu-id="faefa-144">There are two fields that you need to update with your app URL.</span></span>

- <span data-ttu-id="faefa-145">Изменить URL-адрес контента на`https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="faefa-145">Change Content URL to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="faefa-146">Измените URL-адрес веб-сайта на`https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="faefa-146">Change Website URL to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="faefa-147">Где `yourteamsapp.ngrok.io` следует заменять на URL-адрес, который вы использовали при размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="faefa-147">Where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="faefa-148">боты;</span><span class="sxs-lookup"><span data-stu-id="faefa-148">Bots</span></span>

<span data-ttu-id="faefa-149">Боты — это наиболее распространенный способ добавления функциональных возможностей в приложение.</span><span class="sxs-lookup"><span data-stu-id="faefa-149">Bots are the most common way to add functionality to your app.</span></span> <span data-ttu-id="faefa-150">В примере Hello World уже есть Bot в составе примера, но он пока не зарегистрирован в Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="faefa-150">The hello world sample already has a bot as part of the sample, but it has not been registered with Microsoft yet.</span></span>

<img  width="450px" title="Добавление ленты" src="~/assets/images/get-started/app-studio-manifest-editor-bots.png"/>

<span data-ttu-id="faefa-152">У ленты, импортированной из примера, нет идентификатора приложения, связанного с ним.</span><span class="sxs-lookup"><span data-stu-id="faefa-152">The bot that was imported from the sample does not have an App ID associated with it yet.</span></span> <span data-ttu-id="faefa-153">Вам потребуется создать новый робот, чтобы приложение App Studio могло создать новый идентификатор приложения и зарегистрировать его в корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="faefa-153">You will have to create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span> <span data-ttu-id="faefa-154">Обратите внимание, что это идентификатор приложения для Bot, который отличается от идентификатора приложения, созданного для приложения на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="faefa-154">Note that this is the App ID for the bot, which is different from the App ID that we created for the app in a earlier step.</span></span> <span data-ttu-id="faefa-155">Каждому интерфейсу Bot в приложении необходим свой идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="faefa-155">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="faefa-156">Нажмите кнопку *Удалить* рядом с *импортированной* страницей ленты в списке "bot".</span><span class="sxs-lookup"><span data-stu-id="faefa-156">Click the *delete* button next to the *Imported bot* in the bot list.</span></span>

<span data-ttu-id="faefa-157">Теперь нет Боты, оставшихся для отображения.</span><span class="sxs-lookup"><span data-stu-id="faefa-157">Now there are no bots left to show.</span></span> <span data-ttu-id="faefa-158">Нажмите кнопку *Настройка*.</span><span class="sxs-lookup"><span data-stu-id="faefa-158">Click *Setup*.</span></span> <span data-ttu-id="faefa-159">Отобразится диалоговое окно *Настройка ленты* .</span><span class="sxs-lookup"><span data-stu-id="faefa-159">This will display the *Set up a bot* dialog.</span></span>

<img  width="450px" title="Добавление диалогового окна "bot"" src="~/assets/images/get-started/app-studio-manifest-editor-bots-setup-dialog.png"/>

<span data-ttu-id="faefa-161">Добавьте имя Bot `Contoso bot`, например, и нажмите обе кнопки в разделе *область*.</span><span class="sxs-lookup"><span data-stu-id="faefa-161">Add a bot name such as `Contoso bot`, and click both the buttons under *scope*.</span></span>

<span data-ttu-id="faefa-162">Нажмите кнопку *создать Bot* , чтобы выйти из диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="faefa-162">Choose *Create bot* to exit the dialog.</span></span> <span data-ttu-id="faefa-163">Приложение Studio Studio потратит время на регистрацию ленты в Майкрософт, а затем отобразит новый элемент Bot в списке "bot".</span><span class="sxs-lookup"><span data-stu-id="faefa-163">App Studio will spend a moment registering your bot with Microsoft, and then should display your new bot in the bot list.</span></span> <span data-ttu-id="faefa-164">Теперь самое время открыть текстовый файл в блокноте и скопировать и вставить в него новый идентификатор Bot.</span><span class="sxs-lookup"><span data-stu-id="faefa-164">Now would be a good time to open a text file in notepad and copy and paste your new bot id into it.</span></span> <span data-ttu-id="faefa-165">Этот идентификатор потребуется позже.</span><span class="sxs-lookup"><span data-stu-id="faefa-165">You will need this id later.</span></span>

<span data-ttu-id="faefa-166">Нажмите *создать новый пароль*и запишите пароль в том же текстовом файле, в котором был указан идентификатор приложения для ленты.</span><span class="sxs-lookup"><span data-stu-id="faefa-166">Click *Generate New Password*, and make a note of the password in the same text file you noted your Bot app ID in.</span></span> <span data-ttu-id="faefa-167">Это единственный срок, в течение которого будет отображаться пароль, поэтому обязательно сделайте это сейчас.</span><span class="sxs-lookup"><span data-stu-id="faefa-167">This is the only time your password will be shown, so be sure to do this now.</span></span>

<span data-ttu-id="faefa-168">Измените *адрес конечной точки ленты* `https://yourteamsapp.ngrok.io/api/messages`, `yourteamsapp.ngrok.io` указав URL-адрес, который вы использовали при размещении приложения.</span><span class="sxs-lookup"><span data-stu-id="faefa-168">Update the *Bot endpoint address* to `https://yourteamsapp.ngrok.io/api/messages`, where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

<span data-ttu-id="faefa-169">Теперь рекомендуется сохранить текстовый файл, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="faefa-169">Now would be a good time to save your text file if you have not done so already.</span></span> <span data-ttu-id="faefa-170">Вы добавите эти сведения в размещенное приложение позже в этом пошаговом руководстве, которое позволит защитить связь с сервером Bot.</span><span class="sxs-lookup"><span data-stu-id="faefa-170">You will add this information to your hosted app later in this walkthrough, which will allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="faefa-171">расширения для обмена сообщениями;</span><span class="sxs-lookup"><span data-stu-id="faefa-171">Messaging extensions</span></span>

<span data-ttu-id="faefa-172">Расширения обмена сообщениями позволяют пользователям запрашивать информацию из вашей службы и отправлять эти сведения в форме карточек прямо в беседу канала.</span><span class="sxs-lookup"><span data-stu-id="faefa-172">Messaging extensions let users ask for information from your service and post that information, in the form of cards, right into the channel conversation.</span></span> <span data-ttu-id="faefa-173">Расширения обмена сообщениями отображаются в нижней части поля "создание".</span><span class="sxs-lookup"><span data-stu-id="faefa-173">Messaging extensions appear along the bottom of the compose box.</span></span>

<span data-ttu-id="faefa-174">Чтобы приступить к настройке расширения системы обмена сообщениями, щелкните ссылку *расширения системы обмена сообщениями* в разделе *возможности* в левом столбце приложения Studio.</span><span class="sxs-lookup"><span data-stu-id="faefa-174">Click on *Messaging extensions* under *Capabilities* in the left hand column of App Studio to begin configuring the messaging extension.</span></span>

<img  width="450px" title="Добавление расширения обмена сообщениями" src="~/assets/images/get-started/app-studio-manifest-editor-mess-ext.png"/>

<span data-ttu-id="faefa-176">Образец расширения обмена сообщениями отображается в области справа в разделе *расширения обмена сообщениями*.</span><span class="sxs-lookup"><span data-stu-id="faefa-176">The sample messaging extension is listed in the right hand pane under *Messaging Extensions*.</span></span> <span data-ttu-id="faefa-177">Нажмите кнопку *Удалить* еще раз, чтобы удалить эту запись, а затем нажмите кнопку *настроить* , чтобы выполнить те же действия, что и для Боты.</span><span class="sxs-lookup"><span data-stu-id="faefa-177">Click *Delete* again to remove this entry, and then click the *Set up* button following the same steps as you followed for bots.</span></span> <span data-ttu-id="faefa-178">Отобразится диалоговое окно *расширения сообщения* .</span><span class="sxs-lookup"><span data-stu-id="faefa-178">This will display the *Messaging Extension* dialog.</span></span>

<span data-ttu-id="faefa-179">Установите флажок *использовать существующую вкладку ленты* , а затем *выберите один из существующих Боты*.</span><span class="sxs-lookup"><span data-stu-id="faefa-179">Select the *Use existing bot* tab, then *Select from one of my existing bots*.</span></span> <span data-ttu-id="faefa-180">В раскрывающемся меню выберите элемент Bot, созданный в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="faefa-180">In the drop-down menu, select the bot you created in the section above.</span></span> <span data-ttu-id="faefa-181">Добавьте *имя Bot* и нажмите кнопку *сохранить* , чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="faefa-181">Add a *Bot name* and click *Save* to close the dialog.</span></span>

<span data-ttu-id="faefa-182">В разделе *команда* нажмите кнопку *Добавить*.</span><span class="sxs-lookup"><span data-stu-id="faefa-182">Under the *Command* section, click *Add*.</span></span> <span data-ttu-id="faefa-183">Мы добавим команду на основе поиска, поэтому выберите параметр *Разрешить пользователям запрашивать службу...* .</span><span class="sxs-lookup"><span data-stu-id="faefa-183">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span></span>

<span data-ttu-id="faefa-184">В диалоговом окне *Создание команды* введите указанные ниже значения.</span><span class="sxs-lookup"><span data-stu-id="faefa-184">In the *New command* dialog enter the following values.</span></span>

<span data-ttu-id="faefa-185">В разделе *Новая команда*:</span><span class="sxs-lookup"><span data-stu-id="faefa-185">Under *New command*:</span></span>

- <span data-ttu-id="faefa-186">*Идентификатор команды* = жетрандомтекст</span><span class="sxs-lookup"><span data-stu-id="faefa-186">*Command ID*  = getRandomText</span></span>
- <span data-ttu-id="faefa-187">*Title* = получить некоторый произвольный текст для развлечений</span><span class="sxs-lookup"><span data-stu-id="faefa-187">*Title*       = Get some random text for fun</span></span>
- <span data-ttu-id="faefa-188">*Description* = получает произвольный текст и изображения</span><span class="sxs-lookup"><span data-stu-id="faefa-188">*Description* = Gets some random text and images</span></span>

<span data-ttu-id="faefa-189">В разделе *параметр*:</span><span class="sxs-lookup"><span data-stu-id="faefa-189">Under *Parameter*:</span></span>

- <span data-ttu-id="faefa-190">*Name* = кардтитле</span><span class="sxs-lookup"><span data-stu-id="faefa-190">*Name*        = cardTitle</span></span>
- <span data-ttu-id="faefa-191">*Title* = название карточки</span><span class="sxs-lookup"><span data-stu-id="faefa-191">*Title*       = Card title</span></span>
- <span data-ttu-id="faefa-192">*Description* = название карты, которое будет использоваться</span><span class="sxs-lookup"><span data-stu-id="faefa-192">*Description* = Card title to use</span></span>

<span data-ttu-id="faefa-193">После ввода данных нажмите кнопку *сохранить* , чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="faefa-193">Once you're entered the information, click *Save* to close the dialog.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="faefa-194">Регистрация приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="faefa-194">Register your app in Teams</span></span>

<span data-ttu-id="faefa-195">Теперь вы ввели сведения о вашем приложении, но не можете выполнить два действия.</span><span class="sxs-lookup"><span data-stu-id="faefa-195">You have now completed entering the details of your app, but two steps remain.</span></span> <span data-ttu-id="faefa-196">Сначала необходимо использовать раздел "тестирование и распределение" приложения "App Studio", чтобы установить приложение в Teams, а затем необходимо обновить размещенное приложение с помощью идентификатора приложения и пароля для ленты.</span><span class="sxs-lookup"><span data-stu-id="faefa-196">First you must use the Test and Distribute section of App Studio to install your app in Teams, and second you must update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="faefa-197">Помните, что в примере предполагается использование одного и того же идентификатора и пароля приложения для почтового расширения Bot и сообщения.</span><span class="sxs-lookup"><span data-stu-id="faefa-197">Remember that the sample expects to use the same App ID and password for both the bot and the messaging extension.</span></span>

<span data-ttu-id="faefa-198">Щелкните *тест и распределить* элемент под заголовком *Готово* в левом столбце App Studio.</span><span class="sxs-lookup"><span data-stu-id="faefa-198">Click on the *Test and distribute* item under *Finish* in the left hand column of App Studio.</span></span>

<img  width="450px" title="Тестирование приложения" src="~/assets/images/get-started/app-studio-manifest-editor-test.png"/>

<span data-ttu-id="faefa-200">Чтобы отправить приложение в Teams, нажмите кнопку *установить* в разделе *Проверка и распространение*.</span><span class="sxs-lookup"><span data-stu-id="faefa-200">In order to upload your app to Teams, click the *Install* button under *Test and Distribute*.</span></span>

<img  width="450px" title="Добавление диалогового окна расширения обмена сообщениями" src="~/assets/images/get-started/app-studio-manifest-editor-test-dialog.png"/>

<span data-ttu-id="faefa-202">Щелкните поле *поиска* в разделе *Добавить в группу* и выберите группу, в которую добавляется пример приложения.</span><span class="sxs-lookup"><span data-stu-id="faefa-202">Click on the *Search* box in the *Add to a team* section and select a team to add the sample app to.</span></span> <span data-ttu-id="faefa-203">Обычно для тестирования потребуется настроить специальную команду.</span><span class="sxs-lookup"><span data-stu-id="faefa-203">Usually you will want to set up a special team for testing.</span></span>

<span data-ttu-id="faefa-204">Нажмите кнопку *Install (установить* ) в нижней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="faefa-204">Click the *Install* button at the bottom of the dialog.</span></span>

<span data-ttu-id="faefa-205">В этом пошаговом руководстве для App Studio будет завершена эта часть.</span><span class="sxs-lookup"><span data-stu-id="faefa-205">This finishes the App Studio portion of this walkthrough.</span></span> <span data-ttu-id="faefa-206">Теперь вы должны увидеть ваше приложение, работающее в Teams, но не будет работать, пока вы не обновите среду размещенных приложений, чтобы узнать, какие идентификаторы и пароли приложений.</span><span class="sxs-lookup"><span data-stu-id="faefa-206">You should now see your app running in Teams, however the bot and the messaging extension will not work until you update the hosted applications environment to know what the App IDs and passwords are.</span></span>

<img  width="450px" title="Законченное приложение" src="~/assets/images/get-started/app-studio-finished-app.png"/>