### <a name="_layoutcshtml"></a><span data-ttu-id="2eb1b-101">_Layout. cshtml</span><span class="sxs-lookup"><span data-stu-id="2eb1b-101">_Layout.cshtml</span></span>

<span data-ttu-id="2eb1b-102">Чтобы вкладка отображалась в Teams, необходимо включить **клиентский пакет SDK Microsoft Teams для JavaScript** и включить вызов `microsoftTeams.initialize()` после загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="2eb1b-103">Это способ общения вкладки и клиента teams:</span><span class="sxs-lookup"><span data-stu-id="2eb1b-103">This is how your tab and the Teams client communicate:</span></span>

- <span data-ttu-id="2eb1b-104">Перейдите к **общей** папке, откройте **_layout. cshtml** и добавьте следующий `<head>` тег в тег:</span><span class="sxs-lookup"><span data-stu-id="2eb1b-104">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
><span data-ttu-id="2eb1b-105">Не копируйте `<script src="...">` URL-адреса с этой страницы, так как они могут не представлять последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-105">Don't copy/paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="2eb1b-106">Чтобы получить последнюю версию пакета SDK, всегда переходите по адресу: [API JavaScript для Microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js).</span><span class="sxs-lookup"><span data-stu-id="2eb1b-106">To get the latest version of the SDK, always go to: [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="2eb1b-107">TAB. cshtml</span><span class="sxs-lookup"><span data-stu-id="2eb1b-107">Tab.cshtml</span></span>

<span data-ttu-id="2eb1b-108">Откройте **вкладку. cshtml** и обновите внедренный код `<script>` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2eb1b-108">Open **Tab.cshtml** and update the embedded `<script>` as follows:</span></span>

- <span data-ttu-id="2eb1b-109">В верхней части сценария вызовите метод `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="2eb1b-109">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

- <span data-ttu-id="2eb1b-110">Обновите `websiteUrl` `contentUrl` значения и значения в каждой функции с помощью URL-адреса ngrok HTTPS на вкладке.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-110">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

<span data-ttu-id="2eb1b-111">Теперь код должен выглядеть следующим образом с помощью **y8rCgT2b** , заменяя URL-адресом ngrok:</span><span class="sxs-lookup"><span data-stu-id="2eb1b-111">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

```javascript
    microsoftTeams.initialize();

    let saveGray = () => {
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            microsoftTeams.settings.setSettings({
                websiteUrl: `https://y8rCgT2b.ngrok.io`,
                contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                entityId: "grayIconTab",
                suggestedDisplayName: "MyNewTab"
            });
            saveEvent.notifySuccess();
        });
    }

    let saveRed = () => {
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            microsoftTeams.settings.setSettings({
                websiteUrl: `https://y8rCgT2b.ngrok.io`,
                contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                entityId: "redIconTab",
                suggestedDisplayName: "MyNewTab"
            });
            saveEvent.notifySuccess();
        });
    }
```

<span data-ttu-id="2eb1b-112">Обязательно сохраните обновленный элемент **TAB. cshtml**.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-112">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="2eb1b-113">Построение и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="2eb1b-113">Build and run your application</span></span>

- <span data-ttu-id="2eb1b-114">В Visual Studio нажмите клавишу **F5** или в меню **Отладка** выберите команду **начать отладку** .</span><span class="sxs-lookup"><span data-stu-id="2eb1b-114">In Visual Studio press **F5**, or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="2eb1b-115">Убедитесь, что **ngrok** работает и правильно работает, открыв браузер и перейдя на страницу содержимого с помощью URL-адреса ngrok HTTPS, который был предоставлен в окне командной строки.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-115">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="2eb1b-116">Для выполнения этого краткого руководства необходимо одновременное выполнение приложения в Visual Studio и ngrok.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-116">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="2eb1b-117">Если вам нужно прекратить работу приложения в Visual Studio для работы с ним, **продолжите работу ngrok**.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-117">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="2eb1b-118">Он будет продолжать прослушивать и возобновить маршрутизацию запроса приложения при его перезапуске в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-118">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="2eb1b-119">Если вам потребуется перезапустить службу ngrok, она вернет новый URL-адрес, и вам потребуется обновить свое приложение с помощью нового URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-119">If you have to restart the ngrok service it will return a new URL and you'll have to update your application with the new URL.</span></span>

## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="2eb1b-120">Отправка вкладки в Teams с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="2eb1b-120">Upload your tab to Teams with App Studio</span></span>

>[!Note]
> <span data-ttu-id="2eb1b-121">Мы используем приложение App Studio, чтобы изменить **manifest.jsдля** файла и отправить завершенный пакет в Teams.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-121">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="2eb1b-122">Вы также можете вручную изменить **manifest.jsдля** файла, если вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-122">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="2eb1b-123">Если вы сделаете это, не забудьте создать решение еще раз, чтобы создать файл **tab.zip** для отправки.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-123">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="2eb1b-124">Откройте клиент Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-124">Open the Microsoft Teams client.</span></span> <span data-ttu-id="2eb1b-125">Если вы используете [версию на основе веб-сайта](https://teams.microsoft.com) , вы можете проверить интерфейсный код с помощью [средств разработчика](~/tabs/how-to/developer-tools.md)в браузере.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-125">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="2eb1b-126">Откройте приложение App Studio и выберите вкладку **редактор манифестов** .</span><span class="sxs-lookup"><span data-stu-id="2eb1b-126">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="2eb1b-127">В редакторе манифеста выберите **импортировать существующую** плитку приложения, чтобы начать обновление пакета приложения для вкладки. Исходный код сопровождается собственным частично завершенным манифестом.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-127">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="2eb1b-128">Имя пакета приложения **tab.zip**.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-128">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="2eb1b-129">Его можно найти здесь:</span><span class="sxs-lookup"><span data-stu-id="2eb1b-129">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- <span data-ttu-id="2eb1b-130">Отправьте **tab.zip** в приложение App Studio.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-130">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="2eb1b-131">Обновление пакета приложения с помощью редактора манифеста</span><span class="sxs-lookup"><span data-stu-id="2eb1b-131">Update your app package with Manifest editor</span></span>

<span data-ttu-id="2eb1b-132">После того как вы отправили пакет приложений в приложение App Studio, вам потребуется завершить его настройку.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-132">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="2eb1b-133">На правой панели страницы приветствия редактора манифеста выберите плитку для вновь импортированной вкладки.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-133">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="2eb1b-134">В левой части редактора манифеста есть список действий, а справа — список свойств, значения которых должны быть заданы для каждого из этих шагов.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-134">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="2eb1b-135">В *manifest.js* включены многие сведения, но существует несколько полей, которые необходимо обновить:</span><span class="sxs-lookup"><span data-stu-id="2eb1b-135">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="2eb1b-136">Сведения: сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="2eb1b-136">Details: App details</span></span>

- <span data-ttu-id="2eb1b-137">В разделе *Идентификация* выберите \***создать** _, чтобы заменить замещающий идентификатор на нужный идентификатор GUID для вкладки.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-137">Under *Identification* select \***Generate** _ to replace the placeholder id with the required GUID for your tab.</span></span>

- <span data-ttu-id="2eb1b-138">В разделе сведения о _Developer \* обновите поле **URL-адрес веб-сайта** с помощью URL-адреса *ngrok* HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-138">Under _Developer information\* update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="2eb1b-139">В разделе *URL-адреса приложений* обновите заявление **о конфиденциальности** и **условия использования** URL-адресов с помощью URL-адреса *ngrok* HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-139">Under *App URLs* update the **Privacy statement** and **Terms of use** URL fields with your *ngrok* HTTPS URL.</span></span> <span data-ttu-id="2eb1b-140">Не забудьте включить пути */приваци* и */Тау* в конце URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-140">Remember to include the */privacy* and */tou* paths at the end of the URLs.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="2eb1b-141">Возможности: вкладки</span><span class="sxs-lookup"><span data-stu-id="2eb1b-141">Capabilities: Tabs</span></span>

<span data-ttu-id="2eb1b-142">В разделе *вкладки* :</span><span class="sxs-lookup"><span data-stu-id="2eb1b-142">In the *Tabs* section:</span></span>

- <span data-ttu-id="2eb1b-143">На *вкладке Группа* нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-143">Under *Team Tab* select **Add**.</span></span>

- <span data-ttu-id="2eb1b-144">Во всплывающем окне вкладки команды обновите *URL-адрес конфигурации* до `https://<yourngrokurl>/tab` .</span><span class="sxs-lookup"><span data-stu-id="2eb1b-144">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="2eb1b-145">И, наконец, убедитесь, что вы *можете обновить конфигурацию? Флажки группа и* *Групповая беседа* отмечены и нажмите кнопку **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-145">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="2eb1b-146">Готово: домены и разрешения</span><span class="sxs-lookup"><span data-stu-id="2eb1b-146">Finish: Domains and permissions</span></span>

<span data-ttu-id="2eb1b-147">В разделе *домены и разрешения* *домены из поля вкладки* должны содержать URL-адрес NGROK без префикса HTTPS `<yourngrokurl>.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="2eb1b-147">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="test-and-distribute-test-and-distribute"></a><span data-ttu-id="2eb1b-148">Тестирование и распределение: тестирование и распределение</span><span class="sxs-lookup"><span data-stu-id="2eb1b-148">Test and distribute: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="2eb1b-149">В поле **Описание** справа появится следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="2eb1b-149">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="2eb1b-150">&#9888; "**массив" валиддомаинс "не может содержать туннельный сайт...**"</span><span class="sxs-lookup"><span data-stu-id="2eb1b-150">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="2eb1b-151">Это предупреждение можно игнорировать при тестировании вкладки.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-151">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="2eb1b-152">В разделе " *тестирование и распространение* ":</span><span class="sxs-lookup"><span data-stu-id="2eb1b-152">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="2eb1b-153">Нажать кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-153">Select **Install**.</span></span>

- <span data-ttu-id="2eb1b-154">Во всплывающем окне *Добавление в группу или в* поле "разговор" введите команду и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-154">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="2eb1b-155">В следующем всплывающем окне выберите канал команды, в котором будет отображаться вкладка, и нажмите кнопку **настроить**.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-155">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="2eb1b-156">В последнем всплывающем окне выберите значение для вкладки (красный или серый значок) и нажмите кнопку **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-156">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="2eb1b-157">Чтобы просмотреть вкладку, перейдите к группе, в которой она была установлена, и выберите ее в панели вкладок.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-157">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="2eb1b-158">Должна отобразиться страница, выбранная во время настройки.</span><span class="sxs-lookup"><span data-stu-id="2eb1b-158">The page that you chose during configuration should be displayed.</span></span>
