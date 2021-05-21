## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="3a731-101">Upload вкладку для Teams в App Studio</span><span class="sxs-lookup"><span data-stu-id="3a731-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="3a731-102">Мы используем App Studio для редактирования **manifest.jsфайла** и отправки завершенного пакета в Teams.</span><span class="sxs-lookup"><span data-stu-id="3a731-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="3a731-103">Вы также можете вручную **редактироватьmanifest.js,** если хотите.</span><span class="sxs-lookup"><span data-stu-id="3a731-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="3a731-104">Если это так, обязательно создайте решение снова, чтобы создатьTab.zip **файл** для загрузки.</span><span class="sxs-lookup"><span data-stu-id="3a731-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="3a731-105">Откройте Microsoft Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="3a731-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="3a731-106">Если вы используете [веб-версию,](https://teams.microsoft.com) вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="3a731-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="3a731-107">Откройте студию Приложения и выберите **вкладку редактора Манифеста.**</span><span class="sxs-lookup"><span data-stu-id="3a731-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="3a731-108">Выберите импорт **существующей плитки** приложения в редакторе Манифест, чтобы приступить к обновлению пакета приложений для вкладки. Исходный код поставляется со своим частично полным манифестом.</span><span class="sxs-lookup"><span data-stu-id="3a731-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="3a731-109">Имя вашего пакета приложений **tab.zip**.</span><span class="sxs-lookup"><span data-stu-id="3a731-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="3a731-110">Его следует найти здесь:</span><span class="sxs-lookup"><span data-stu-id="3a731-110">It should be found here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/Tab.zip
    ```

- <span data-ttu-id="3a731-111">Upload **Tab.zip** App Studio.</span><span class="sxs-lookup"><span data-stu-id="3a731-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="3a731-112">Обновление пакета приложений с помощью редактора Manifest</span><span class="sxs-lookup"><span data-stu-id="3a731-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="3a731-113">После отправки пакета приложения в App Studio необходимо завершить его настройку.</span><span class="sxs-lookup"><span data-stu-id="3a731-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="3a731-114">Выберите плитку для недавно импортируемой вкладки в правой панели приветствия редактора Манифеста.</span><span class="sxs-lookup"><span data-stu-id="3a731-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="3a731-115">В левой части редактора Манифеста есть список действий, а справа — список свойств, которые должны иметь значения для каждого из этих действий.</span><span class="sxs-lookup"><span data-stu-id="3a731-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="3a731-116">Большая часть сведений предоставлена вашими *manifest.js,* но есть несколько полей, которые необходимо обновить:</span><span class="sxs-lookup"><span data-stu-id="3a731-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="3a731-117">Сведения: сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="3a731-117">Details: App details</span></span>

<span data-ttu-id="3a731-118">В разделе **Сведения о приложении:**</span><span class="sxs-lookup"><span data-stu-id="3a731-118">In the **App details** section:</span></span>

- <span data-ttu-id="3a731-119">В **соответствии с определением** **выберите Создание** для создания нового удостоверения приложения для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="3a731-119">Under **Identification** select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="3a731-120">В **статье Сведения разработчика** обновите **URL-адрес веб-сайта** с **помощью URL-адреса HTTPS ngrok.**</span><span class="sxs-lookup"><span data-stu-id="3a731-120">Under **Developer information** update the **Website URL** with your **ngrok** HTTPS URL.</span></span>

- <span data-ttu-id="3a731-121">В **URL-адресах** приложений обновляются **выписки о** конфиденциальности и условия использования для `https://<yourngrokurl>/privacy`  `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="3a731-121">Under **App URLs** update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="3a731-122">Возможности: Вкладки</span><span class="sxs-lookup"><span data-stu-id="3a731-122">Capabilities: Tabs</span></span>

<span data-ttu-id="3a731-123">В разделе *Tabs:*</span><span class="sxs-lookup"><span data-stu-id="3a731-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="3a731-124">В **статье Добавить личную вкладку** выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a731-124">Under **Add a personal tab** select **Add**.</span></span> <span data-ttu-id="3a731-125">Вам будет представлено всплывающее окно диалогов.</span><span class="sxs-lookup"><span data-stu-id="3a731-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="3a731-126">Заполни **поле Имя.**</span><span class="sxs-lookup"><span data-stu-id="3a731-126">Complete the **Name** field.</span></span>

- <span data-ttu-id="3a731-127">Заполни **поле Entity Id.**</span><span class="sxs-lookup"><span data-stu-id="3a731-127">Complete the **Entity Id** field.</span></span>

- <span data-ttu-id="3a731-128">Обновление поля **URL-адресов** контента с помощью `https://<yourngrokurl>/personalTab` .</span><span class="sxs-lookup"><span data-stu-id="3a731-128">Update the **Content URL** field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="3a731-129">Оставьте **поле URL-адрес веб-сайта** пустым.</span><span class="sxs-lookup"><span data-stu-id="3a731-129">Leave the **Website URL** field blank.</span></span>

- <span data-ttu-id="3a731-130">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3a731-130">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="3a731-131">Finish: Домены и разрешения</span><span class="sxs-lookup"><span data-stu-id="3a731-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="3a731-132">В разделе **Домены** и разрешения  домены из поля вкладок должны содержать URL-адрес ngrok без префикса HTTPS `<yourngrokurl>.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="3a731-132">In the **Domains and permissions** section, the **Domains from your tabs** field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="3a731-133">Finish: Test and distribute</span><span class="sxs-lookup"><span data-stu-id="3a731-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="3a731-134">В поле **Описание** справа вы увидите следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="3a731-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="3a731-135">&#9888; массив **"validDomains"** не может содержать сайт тоннелей... "</span><span class="sxs-lookup"><span data-stu-id="3a731-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="3a731-136">Это предупреждение можно игнорировать при тестировании вкладки.</span><span class="sxs-lookup"><span data-stu-id="3a731-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="3a731-137">В разделе **Тест и распространение:**</span><span class="sxs-lookup"><span data-stu-id="3a731-137">In the **Test and distribute** section:</span></span>

- <span data-ttu-id="3a731-138">Нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="3a731-138">Select **Install**.</span></span>

- <span data-ttu-id="3a731-139">В всплывающее окно убедитесь, что **добавить** для вас задают да и добавить в команду или **чат** задайте **нет**. </span><span class="sxs-lookup"><span data-stu-id="3a731-139">In the pop-up window make sure that **Add for you** is set to **Yes** and **Add to a team or chat** is set to **No**.</span></span>

- <span data-ttu-id="3a731-140">Нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="3a731-140">Select **Install**.</span></span>

- <span data-ttu-id="3a731-141">В следующем всплывающее окно выберите **Открыть,** и вкладка будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="3a731-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="3a731-142">Просмотр личной вкладки</span><span class="sxs-lookup"><span data-stu-id="3a731-142">View your personal tab</span></span>

- <span data-ttu-id="3a731-143">В панели навигации, расположенной слева от Teams app, выберите `...` меню.</span><span class="sxs-lookup"><span data-stu-id="3a731-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="3a731-144">Вам будет представлен список личных приложений.</span><span class="sxs-lookup"><span data-stu-id="3a731-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="3a731-145">Выберите вкладку из списка для просмотра.</span><span class="sxs-lookup"><span data-stu-id="3a731-145">Select your tab from the list to view.</span></span>
