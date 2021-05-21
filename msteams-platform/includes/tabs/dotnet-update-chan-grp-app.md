### <a name="_layoutcshtml"></a><span data-ttu-id="bd6c6-101">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="bd6c6-101">_Layout.cshtml</span></span>

<span data-ttu-id="bd6c6-102">Чтобы вкладка отображалась в Teams, необходимо включить Microsoft Teams **клиента JavaScript** и включить вызов после загрузки `microsoftTeams.initialize()` страницы.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="bd6c6-103">Это то, как ваша вкладка и Teams клиент:</span><span class="sxs-lookup"><span data-stu-id="bd6c6-103">This is how your tab and the Teams client communicate:</span></span>

- <span data-ttu-id="bd6c6-104">Перейдите в **общую** папку, **откройте _Layout.cshtml** и добавьте в тег `<head>` следующее:</span><span class="sxs-lookup"><span data-stu-id="bd6c6-104">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

>[!IMPORTANT]
><span data-ttu-id="bd6c6-105">Не копируйте и не вдайте URL-адреса на этой странице, так как они могут `<script src="...">` не представлять последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-105">Don't copy/paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="bd6c6-106">Чтобы получить последнюю версию SDK, всегда перейдите к: Microsoft Teams [API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).</span><span class="sxs-lookup"><span data-stu-id="bd6c6-106">To get the latest version of the SDK, always go to: [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="bd6c6-107">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="bd6c6-107">Tab.cshtml</span></span>

<span data-ttu-id="bd6c6-108">Откройте **Tab.cshtml** и обнови встраиваемый элемент `<script>` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bd6c6-108">Open **Tab.cshtml** and update the embedded `<script>` as follows:</span></span>

- <span data-ttu-id="bd6c6-109">В верхней части сценария позвоните `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="bd6c6-109">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

- <span data-ttu-id="bd6c6-110">Обновление `websiteUrl` `contentUrl` значений и значений в каждой функции с ПОМОЩЬЮ URL-адреса https ngrok на вкладке.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-110">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

<span data-ttu-id="bd6c6-111">Теперь код должен выглядеть следующим образом: **y8rCgT2b заменен** на URL-адрес ngrok:</span><span class="sxs-lookup"><span data-stu-id="bd6c6-111">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

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

<span data-ttu-id="bd6c6-112">Обязательно сохраните обновленный **Tab.cshtml.**</span><span class="sxs-lookup"><span data-stu-id="bd6c6-112">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="bd6c6-113">Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="bd6c6-113">Build and run your application</span></span>

- <span data-ttu-id="bd6c6-114">В Visual Studio нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки.**</span><span class="sxs-lookup"><span data-stu-id="bd6c6-114">In Visual Studio press **F5**, or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="bd6c6-115">Убедитесь, что **ngrok** работает и работает должным образом, открыв браузер и переехав на страницу контента через URL-адрес https ngrok, который был представлен в окне командной подсказки.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-115">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="bd6c6-116">Для выполнения этого quickstart необходимо Visual Studio и ngrok.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-116">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="bd6c6-117">Если вам нужно перестать запускать приложение в Visual Studio работать над ней, продолжайте **работать ngrok**.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-117">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="bd6c6-118">После перезапуска в Visual Studio он будет продолжать прослушивать запрос приложения и возобновлять маршрутиза Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-118">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="bd6c6-119">Если вам придется перезапустить службу ngrok, она возвращает новый URL-адрес, и вам придется обновить приложение с помощью нового URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-119">If you have to restart the ngrok service it will return a new URL and you'll have to update your application with the new URL.</span></span>

## <a name="upload-your-tab-to-teams"></a><span data-ttu-id="bd6c6-120">Upload вкладку на Teams</span><span class="sxs-lookup"><span data-stu-id="bd6c6-120">Upload your tab to Teams</span></span>

>[!Note]
> <span data-ttu-id="bd6c6-121">Мы используем App Studio для редактирования **manifest.jsфайла** и отправки завершенного пакета в Teams.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-121">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="bd6c6-122">Вы также можете вручную редактировать **manifest.jsфайл,** если хотите.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-122">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="bd6c6-123">Если это так, обязательно создайте решение снова, чтобы создатьtab.zip **файл** для загрузки.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-123">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="bd6c6-124">Откройте Microsoft Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-124">Open the Microsoft Teams client.</span></span> <span data-ttu-id="bd6c6-125">Если вы используете [веб-версию,](https://teams.microsoft.com) вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="bd6c6-125">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="bd6c6-126">Откройте студию Приложения и выберите **вкладку редактора Манифеста.**</span><span class="sxs-lookup"><span data-stu-id="bd6c6-126">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="bd6c6-127">Выберите импорт **существующей плитки** приложения в редакторе Манифест, чтобы приступить к обновлению пакета приложений для вкладки. Исходный код поставляется со своим частично полным манифестом.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-127">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="bd6c6-128">Имя вашего пакета приложений **tab.zip**.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-128">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="bd6c6-129">Его следует найти здесь:</span><span class="sxs-lookup"><span data-stu-id="bd6c6-129">It should be found here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

- <span data-ttu-id="bd6c6-130">Upload **tab.zip** App Studio.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-130">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="bd6c6-131">Обновление пакета приложений с помощью редактора Manifest</span><span class="sxs-lookup"><span data-stu-id="bd6c6-131">Update your app package with Manifest editor</span></span>

<span data-ttu-id="bd6c6-132">После отправки пакета приложения в App Studio необходимо завершить его настройку.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-132">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="bd6c6-133">Выберите плитку для недавно импортируемой вкладки в правой панели приветствия редактора Манифеста.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-133">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="bd6c6-134">В левой части редактора Манифеста есть список действий, а справа — список свойств, которые должны иметь значения для каждого из этих действий.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-134">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="bd6c6-135">Большая часть сведений предоставлена вашими *manifest.js,* но есть несколько полей, которые необходимо обновить:</span><span class="sxs-lookup"><span data-stu-id="bd6c6-135">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="bd6c6-136">Сведения: сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="bd6c6-136">Details: App details</span></span>

<span data-ttu-id="bd6c6-137">В разделе *Сведения о приложении:*</span><span class="sxs-lookup"><span data-stu-id="bd6c6-137">In the *App details* section:</span></span>

- <span data-ttu-id="bd6c6-138">*Идентификация:* **выберите Создание** для замены удостоверения замещающего удостоверения на необходимый GUID для вкладки.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-138">*Identification*: select **Generate** to replace the placeholder id with the required GUID for your tab.</span></span>

- <span data-ttu-id="bd6c6-139">*Сведения о* разработчике: обновление **URL-адреса** веб-сайта с *помощью URL-адреса https ngrok.*</span><span class="sxs-lookup"><span data-stu-id="bd6c6-139">*Developer information*: update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="bd6c6-140">*URL-адреса* приложений: обновление заявления **о** конфиденциальности и условия использования `https://<yourngrokurl>/privacy` **для** `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-140">*App URLs*: update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="bd6c6-141">Возможности: Вкладки</span><span class="sxs-lookup"><span data-stu-id="bd6c6-141">Capabilities: Tabs</span></span>

<span data-ttu-id="bd6c6-142">В разделе *Tabs:*</span><span class="sxs-lookup"><span data-stu-id="bd6c6-142">In the *Tabs* section:</span></span>

- <span data-ttu-id="bd6c6-143">*Командная вкладка*: выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-143">*Team Tab*: select **Add**.</span></span>

- <span data-ttu-id="bd6c6-144">В всплывающее окно вкладки "Команда" обновим *URL-адрес конфигурации* `https://<yourngrokurl>/tab` до .</span><span class="sxs-lookup"><span data-stu-id="bd6c6-144">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="bd6c6-145">Наконец, убедитесь, что *конфигурация может обновляться? Командные* и *групповые чаты* проверяются и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-145">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="bd6c6-146">Finish: Домены и разрешения</span><span class="sxs-lookup"><span data-stu-id="bd6c6-146">Finish: Domains and permissions</span></span>

<span data-ttu-id="bd6c6-147">В разделе *Домены и разрешения:*</span><span class="sxs-lookup"><span data-stu-id="bd6c6-147">In the *Domains and permissions* section:</span></span>

- <span data-ttu-id="bd6c6-148">Домены *из поля вкладок* должны содержать URL-адрес ngrok без префикса HTTPS `<yourngrokurl>.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="bd6c6-148">The *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="bd6c6-149">Finish: Test and distribute</span><span class="sxs-lookup"><span data-stu-id="bd6c6-149">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="bd6c6-150">В поле **Описание** справа вы увидите следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="bd6c6-150">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="bd6c6-151">&#9888; массив **"validDomains"** не может содержать сайт тоннелей... "</span><span class="sxs-lookup"><span data-stu-id="bd6c6-151">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="bd6c6-152">Это предупреждение можно игнорировать при тестировании вкладки.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-152">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="bd6c6-153">В разделе *Тест и распространение:*</span><span class="sxs-lookup"><span data-stu-id="bd6c6-153">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="bd6c6-154">Нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-154">Select **Install**.</span></span>

- <span data-ttu-id="bd6c6-155">В всплывающее окно  Добавить в команду или поле чата введите свою команду и выберите **Установите**.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-155">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="bd6c6-156">В следующем всплывающее окно выберите канал команды, в котором будет отображаться вкладка, и выберите **Настройка.**</span><span class="sxs-lookup"><span data-stu-id="bd6c6-156">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="bd6c6-157">В окончательном всплывающее окно выберите значение для страницы вкладки (красный или серый значок) и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-157">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="bd6c6-158">Чтобы просмотреть вкладку, перейдите к установленной команде и выберите ее из панели вкладок.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-158">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="bd6c6-159">Страница, выбранная во время настройки, должна отображаться.</span><span class="sxs-lookup"><span data-stu-id="bd6c6-159">The page that you chose during configuration should be displayed.</span></span>
