## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="bb6ca-101">Upload вкладку, чтобы Teams с App Studio</span><span class="sxs-lookup"><span data-stu-id="bb6ca-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="bb6ca-102">Мы используем App Studio для редактирования **вашихmanifest.jsв файле** и загрузки завершенного пакета Teams.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="bb6ca-103">Вы также можете вручную редактировать **manifest.js, если** вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="bb6ca-104">Если вы это сделаете, не забудьте построить решение снова, чтобы **создатьTab.zip** файл для загрузки.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="bb6ca-105">Откройте Microsoft Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="bb6ca-106">Если вы [используете веб-версию,](https://teams.microsoft.com) вы можете проверить свой передний код с помощью инструментов [разработчика браузера.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="bb6ca-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="bb6ca-107">Откройте студию Приложений и выберите **вкладку редактора** Manifest.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="bb6ca-108">Выберите **импорт существующей плитки** приложения в редакторе Manifest, чтобы начать обновление пакета приложений для вкладки. Исходный код поставляется со своим частично полным манифестом.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="bb6ca-109">Название пакета приложений не **называетсяtab.zip.**</span><span class="sxs-lookup"><span data-stu-id="bb6ca-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="bb6ca-110">Он должен быть найден здесь:</span><span class="sxs-lookup"><span data-stu-id="bb6ca-110">It should be found here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/Tab.zip
    ```

- <span data-ttu-id="bb6ca-111">UploadTab.zip **в** App Studio.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="bb6ca-112">Обновление пакета приложений с редактором Manifest</span><span class="sxs-lookup"><span data-stu-id="bb6ca-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="bb6ca-113">После загрузки пакета приложения в App Studio необходимо закончить его настройку.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="bb6ca-114">Выберите плитку для недавно импортированной вкладки в правой панели страницы приветствия редактора Manifest.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="bb6ca-115">В левой части редактора Manifest есть список шагов, а справа — список свойств, которые должны иметь значения для каждого из этих шагов.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="bb6ca-116">Большая часть информации была предоставлена *вашимиmanifest.js,* но есть несколько полей, которые вам нужно обновить:</span><span class="sxs-lookup"><span data-stu-id="bb6ca-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="bb6ca-117">Подробности: Подробности приложения</span><span class="sxs-lookup"><span data-stu-id="bb6ca-117">Details: App details</span></span>

<span data-ttu-id="bb6ca-118">В разделе **подробностей** приложения:</span><span class="sxs-lookup"><span data-stu-id="bb6ca-118">In the **App details** section:</span></span>

- <span data-ttu-id="bb6ca-119">В **рамках идентификации** **выберите Generate** для создания нового Идентификатора Приложения для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-119">Under **Identification** select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="bb6ca-120">Под **информацией разработчика** **обновить URL-адрес** веб-сайта **с ngrok** HTTPS URL.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-120">Under **Developer information** update the **Website URL** with your **ngrok** HTTPS URL.</span></span>

- <span data-ttu-id="bb6ca-121">В **соответствии с** URL-адресами **приложений обновляйте** `https://<yourngrokurl>/privacy` заявление о **конфиденциальности и условия** использования `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-121">Under **App URLs** update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="bb6ca-122">Возможности: Вкладки</span><span class="sxs-lookup"><span data-stu-id="bb6ca-122">Capabilities: Tabs</span></span>

<span data-ttu-id="bb6ca-123">В разделе *Вкладки:*</span><span class="sxs-lookup"><span data-stu-id="bb6ca-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="bb6ca-124">Под **Добавить личную вкладку** **выберите Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-124">Under **Add a personal tab** select **Add**.</span></span> <span data-ttu-id="bb6ca-125">Вам будет представлено всплывающее окно диалога.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="bb6ca-126">Заполуть **поле** имен.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-126">Complete the **Name** field.</span></span>

- <span data-ttu-id="bb6ca-127">Завершите **поле Entity Id.**</span><span class="sxs-lookup"><span data-stu-id="bb6ca-127">Complete the **Entity Id** field.</span></span>

- <span data-ttu-id="bb6ca-128">Обновление **поля URL-адреса** содержимого с `https://<yourngrokurl>/personalTab` помощью .</span><span class="sxs-lookup"><span data-stu-id="bb6ca-128">Update the **Content URL** field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="bb6ca-129">Оставьте **поле URL-адреса веб-сайта** пустым.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-129">Leave the **Website URL** field blank.</span></span>

- <span data-ttu-id="bb6ca-130">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-130">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="bb6ca-131">Отделка: Домены и разрешения</span><span class="sxs-lookup"><span data-stu-id="bb6ca-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="bb6ca-132">В разделе **Домены и разрешения** **домены из поля вкладок** должны содержать ваш URL ngrok без префикса HTTPS - `<yourngrokurl>.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="bb6ca-132">In the **Domains and permissions** section, the **Domains from your tabs** field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="bb6ca-133">Завершение: Тестирование и распространение</span><span class="sxs-lookup"><span data-stu-id="bb6ca-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="bb6ca-134">В **поле** Описание справа вы увидите следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="bb6ca-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="bb6ca-135">&#9888; "**"ДействительныйДомейнс" массив не может содержать туннель сайт ...**"</span><span class="sxs-lookup"><span data-stu-id="bb6ca-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="bb6ca-136">Это предупреждение может быть проигнорировано при тестировании вкладки.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="bb6ca-137">В разделе **Тест и распространение:**</span><span class="sxs-lookup"><span data-stu-id="bb6ca-137">In the **Test and distribute** section:</span></span>

- <span data-ttu-id="bb6ca-138">Нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-138">Select **Install**.</span></span>

- <span data-ttu-id="bb6ca-139">Во всплывающем окне убедитесь, что **Add for you** установлен на **Да** и Добавить в команду **или чат** установлен в **No**.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-139">In the pop-up window make sure that **Add for you** is set to **Yes** and **Add to a team or chat** is set to **No**.</span></span>

- <span data-ttu-id="bb6ca-140">Нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-140">Select **Install**.</span></span>

- <span data-ttu-id="bb6ca-141">В следующем всплывающем окне выберите **Open и** ваша вкладка будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="bb6ca-142">Просмотр личной вкладки</span><span class="sxs-lookup"><span data-stu-id="bb6ca-142">View your personal tab</span></span>

- <span data-ttu-id="bb6ca-143">В навигационном баре, расположенном слева от приложения Teams, выберите `...` меню.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="bb6ca-144">Вам будет представлен список личных приложений.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="bb6ca-145">Выберите вкладку из списка для просмотра.</span><span class="sxs-lookup"><span data-stu-id="bb6ca-145">Select your tab from the list to view.</span></span>
