### <a name="_layoutcshtml"></a><span data-ttu-id="da236-101">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="da236-101">_Layout.cshtml</span></span>

<span data-ttu-id="da236-102">Чтобы вкладка отображалась в Teams, необходимо включить Microsoft Teams **клиента JavaScript** и включить вызов после загрузки `microsoftTeams.initialize()` страницы.</span><span class="sxs-lookup"><span data-stu-id="da236-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="da236-103">Это то, как ваша вкладка и Teams клиент:</span><span class="sxs-lookup"><span data-stu-id="da236-103">This is how your tab and the Teams client communicate:</span></span>

<span data-ttu-id="da236-104">Перейдите в **общую** папку, **откройте _Layout.cshtml** и добавьте в тег `<head>` следующее:</span><span class="sxs-lookup"><span data-stu-id="da236-104">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
> <span data-ttu-id="da236-105">Не копируйте и не вделайте URL-адреса на этой странице, так как они могут `<script src="...">` не представлять последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="da236-105">Do not copy and paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="da236-106">Чтобы получить последнюю версию SDK, всегда Microsoft Teams [API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).</span><span class="sxs-lookup"><span data-stu-id="da236-106">To get the latest version of the SDK, always go to [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="da236-107">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="da236-107">Tab.cshtml</span></span>

<span data-ttu-id="da236-108">**Обновление встроенного скрипта**</span><span class="sxs-lookup"><span data-stu-id="da236-108">**To update the embedded script**</span></span>

1. <span data-ttu-id="da236-109">В Visual Studio откройте **Tab.cshtml** для обновления встроенного `<script>` .</span><span class="sxs-lookup"><span data-stu-id="da236-109">In Visual Studio, open **Tab.cshtml** to update the embedded `<script>`.</span></span>

1. <span data-ttu-id="da236-110">В верхней части сценария позвоните `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="da236-110">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

1. <span data-ttu-id="da236-111">Обновление `websiteUrl` `contentUrl` значений и значений в каждой функции с ПОМОЩЬЮ URL-адреса https ngrok на вкладке.</span><span class="sxs-lookup"><span data-stu-id="da236-111">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

    <span data-ttu-id="da236-112">Теперь код должен выглядеть следующим образом: **y8rCgT2b заменен** на URL-адрес ngrok:</span><span class="sxs-lookup"><span data-stu-id="da236-112">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

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

1. <span data-ttu-id="da236-113">Обязательно сохраните обновленный **Tab.cshtml.**</span><span class="sxs-lookup"><span data-stu-id="da236-113">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="da236-114">Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="da236-114">Build and run your application</span></span>

<span data-ttu-id="da236-115">В Visual Studio нажмите **кнопку F5** или выберите **Пуск** отладки из меню **отладки.**</span><span class="sxs-lookup"><span data-stu-id="da236-115">In Visual Studio, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="da236-116">Убедитесь, что **ngrok** работает и работает должным образом, открыв браузер и переехав на страницу контента через URL-адрес https ngrok, который был представлен в окне командной подсказки.</span><span class="sxs-lookup"><span data-stu-id="da236-116">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="da236-117">Необходимо, чтобы приложение было запущено как в Visual Studio, так и в ngrok.</span><span class="sxs-lookup"><span data-stu-id="da236-117">You need to have both your application in Visual Studio and ngrok running.</span></span> <span data-ttu-id="da236-118">Если вам нужно перестать запускать приложение в Visual Studio работать над ней, продолжайте **работать ngrok**.</span><span class="sxs-lookup"><span data-stu-id="da236-118">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="da236-119">После перезапуска в Visual Studio он будет продолжать прослушивать запрос приложения и возобновлять маршрутиза Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da236-119">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="da236-120">Если вам придется перезапустить службу ngrok, она возвращает новый URL-адрес, и вам придется обновить приложение с помощью нового URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="da236-120">If you have to restart the ngrok service, it will return a new URL and you will have to update your application with the new URL.</span></span>

## <a name="upload-your-tab"></a><span data-ttu-id="da236-121">Upload вкладку</span><span class="sxs-lookup"><span data-stu-id="da236-121">Upload your tab</span></span>

>[!Note]
> <span data-ttu-id="da236-122">App Studio можно использовать для редактированияmanifest.js **файла** и отправки завершенного пакета в Teams.</span><span class="sxs-lookup"><span data-stu-id="da236-122">App Studio can be used to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="da236-123">Вы также можете вручную редактировать **manifest.jsфайл,** если хотите.</span><span class="sxs-lookup"><span data-stu-id="da236-123">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="da236-124">Если это так, обязательно создайте решение снова, чтобы создатьtab.zip **файл** для загрузки.</span><span class="sxs-lookup"><span data-stu-id="da236-124">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

<span data-ttu-id="da236-125">**Загрузка вкладки**</span><span class="sxs-lookup"><span data-stu-id="da236-125">**To upload your tab**</span></span>

1. <span data-ttu-id="da236-126">Перейдите Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="da236-126">Go to Microsoft Teams.</span></span> <span data-ttu-id="da236-127">Если вы используете [веб-версию,](https://teams.microsoft.com) вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="da236-127">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="da236-128">Перейдите **в App Studio и** выберите **вкладку Редактор Манифеста.**</span><span class="sxs-lookup"><span data-stu-id="da236-128">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="da236-129">Выберите **импорт существующего приложения в** редакторе Манифеста, чтобы приступить к обновлению пакета приложений для вкладки. Исходный код поставляется со своим частично полным манифестом.</span><span class="sxs-lookup"><span data-stu-id="da236-129">Select **Import an existing app** in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="da236-130">Имя вашего пакета приложений **tab.zip**.</span><span class="sxs-lookup"><span data-stu-id="da236-130">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="da236-131">Он доступен здесь:</span><span class="sxs-lookup"><span data-stu-id="da236-131">It is available here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="da236-132">Upload **tab.zip** App Studio.</span><span class="sxs-lookup"><span data-stu-id="da236-132">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="da236-133">Обновление пакета приложений с помощью редактора Manifest</span><span class="sxs-lookup"><span data-stu-id="da236-133">Update your app package with Manifest editor</span></span>

<span data-ttu-id="da236-134">После отправки пакета приложений в App Studio необходимо завершить его настройку.</span><span class="sxs-lookup"><span data-stu-id="da236-134">After you have uploaded your app package into App Studio, you must finish configuring it.</span></span>

<span data-ttu-id="da236-135">Выберите плитку для недавно импортируемой вкладки в правой панели приветствия редактора Манифеста.</span><span class="sxs-lookup"><span data-stu-id="da236-135">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="da236-136">В левой части редактора Манифеста имеется список действий, а справа — список свойств, которые должны иметь значения для каждого из этих действий.</span><span class="sxs-lookup"><span data-stu-id="da236-136">There is a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="da236-137">Большая часть сведений предоставлена вашими **manifest.js,** но есть несколько полей, которые необходимо обновить:</span><span class="sxs-lookup"><span data-stu-id="da236-137">Much of the information has been provided by your **manifest.json** but there are a few fields that you must update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="da236-138">Сведения: сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="da236-138">Details: App details</span></span>

<span data-ttu-id="da236-139">В разделе **Сведения о приложении:**</span><span class="sxs-lookup"><span data-stu-id="da236-139">In the **App details** section:</span></span>

1. <span data-ttu-id="da236-140">В **статье Идентификация** выберите **Создание** для замены удостоверения замещающего удостоверения на необходимый GUID для вкладки.</span><span class="sxs-lookup"><span data-stu-id="da236-140">Under **Identification**, select **Generate** to replace the placeholder ID with the required GUID for your tab.</span></span>

1. <span data-ttu-id="da236-141">В **соответствии с сведениями разработчика** **обновите веб-сайт** **url-адресом https ngrok.**</span><span class="sxs-lookup"><span data-stu-id="da236-141">Under **Developer information**, update **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="da236-142">В **URL-адресах** приложений обнови заявление **конфиденциальности** и условия использования `https://<yourngrokurl>/privacy` **для** `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="da236-142">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="da236-143">Возможности: Вкладки</span><span class="sxs-lookup"><span data-stu-id="da236-143">Capabilities: Tabs</span></span>

<span data-ttu-id="da236-144">В разделе **Tabs:**</span><span class="sxs-lookup"><span data-stu-id="da236-144">In the **Tabs** section:</span></span>

1. <span data-ttu-id="da236-145">В **вкладке Team** выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="da236-145">Under **Team tab**, select **Add**.</span></span>

1. <span data-ttu-id="da236-146">В **всплывающее** окно вкладки "Команда" обнови **URL-адрес конфигурации** `https://<yourngrokurl>/tab` до .</span><span class="sxs-lookup"><span data-stu-id="da236-146">In the **Team tab** pop-up window, update the **Configuration URL** to `https://<yourngrokurl>/tab`.</span></span>

1. <span data-ttu-id="da236-147">Убедитесь, что конфигурация может **обновляться?**, **Командные** и **групповые** почтовые ящики чата выбраны и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="da236-147">Ensure the **Can update configuration?**, **Team**, and **Group chat** checkboxes are selected and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="da236-148">Finish: Домены и разрешения</span><span class="sxs-lookup"><span data-stu-id="da236-148">Finish: Domains and permissions</span></span>

<span data-ttu-id="da236-149">В разделе **Домены и**  разрешения домены с вкладок должны содержать URL-адрес ngrok без префикса `<yourngrokurl>.ngrok.io/` HTTPS.</span><span class="sxs-lookup"><span data-stu-id="da236-149">In the **Domains and permissions** section, **Domains from your tabs** must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="da236-150">Finish: Test and distribute</span><span class="sxs-lookup"><span data-stu-id="da236-150">Finish: Test and distribute</span></span>

>[!IMPORTANT]
> <span data-ttu-id="da236-151">Справа в **описании** см. следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="da236-151">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="da236-152">&#9888; массив **"validDomains"** не может содержать сайт тоннелей... "</span><span class="sxs-lookup"><span data-stu-id="da236-152">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
> <span data-ttu-id="da236-153">Это предупреждение можно игнорировать при тестировании вкладки.</span><span class="sxs-lookup"><span data-stu-id="da236-153">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="da236-154">В разделе **Тест и распространение** выберите **Установите**.</span><span class="sxs-lookup"><span data-stu-id="da236-154">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="da236-155">В диалоговом окне всплывающее окно выберите **Добавить** в команду или из выпадающее окно, выберите **Добавить в чат**.</span><span class="sxs-lookup"><span data-stu-id="da236-155">In the pop-up dialog box, select **Add to a team** or from the drop-down, select **Add to a chat**.</span></span>

1. <span data-ttu-id="da236-156">Выберите команду или чат, где нужно отобразить вкладку, и выберите **Настройка вкладки.**</span><span class="sxs-lookup"><span data-stu-id="da236-156">Choose the team or chat where you want the tab to be displayed and select **Set up a tab**.</span></span>

1. <span data-ttu-id="da236-157">В следующем диалоговом окне всплывающее окно выберите **Выберите серый** или **выберите красный** цвет и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="da236-157">In the next pop-up dialog box, choose either **Select Gray** or **Select Red**, and select **Save**.</span></span>

1. <span data-ttu-id="da236-158">Чтобы просмотреть вкладку, перейдите в команду, в которой установлена вкладка, и выберите ее из панели вкладок.</span><span class="sxs-lookup"><span data-stu-id="da236-158">To view your tab, go to the team where you installed the tab, and select it from the tab bar.</span></span> <span data-ttu-id="da236-159">Отображается страница, выбранная во время настройки.</span><span class="sxs-lookup"><span data-stu-id="da236-159">The page that you chose during configuration is displayed.</span></span>

    ![Загруженная вкладка КАНАЛА ASPNETMVC](../../assets/images/tab-images/channeltabaspnetmvcuploaded.png)

