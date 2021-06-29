## <a name="upload-your-tab-with-app-studio"></a><span data-ttu-id="95442-101">Upload вкладку с Помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="95442-101">Upload your tab with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="95442-102">Мы используем **App Studio** для редактированияmanifest.js **файла** и отправки завершенного пакета в Teams.</span><span class="sxs-lookup"><span data-stu-id="95442-102">We use **App Studio** to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="95442-103">Вы также можете вручную **редактироватьmanifest.js.**</span><span class="sxs-lookup"><span data-stu-id="95442-103">You can also manually edit **manifest.json**.</span></span> <span data-ttu-id="95442-104">Если это так, убедитесь, что вы создайте решение снова, чтобы создатьTab.zip **файл** для загрузки.</span><span class="sxs-lookup"><span data-stu-id="95442-104">If you do, ensure that you build the solution again to create the **Tab.zip** file to upload.</span></span>

<span data-ttu-id="95442-105">**Для загрузки вкладки в App Studio**</span><span class="sxs-lookup"><span data-stu-id="95442-105">**To upload your tab with App Studio**</span></span>

1. <span data-ttu-id="95442-106">Перейдите Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="95442-106">Go to Microsoft Teams.</span></span> <span data-ttu-id="95442-107">Если вы используете [веб-версию,](https://teams.microsoft.com) вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="95442-107">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="95442-108">Перейдите **в App Studio и** выберите **вкладку Редактор Манифеста.**</span><span class="sxs-lookup"><span data-stu-id="95442-108">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="95442-109">Выберите **импорт существующего приложения в** **редакторе Манифеста,** чтобы приступить к обновлению пакета приложений для вкладки. Исходный код поставляется со своим частично полным манифестом.</span><span class="sxs-lookup"><span data-stu-id="95442-109">Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="95442-110">Имя вашего пакета приложений **tab.zip**.</span><span class="sxs-lookup"><span data-stu-id="95442-110">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="95442-111">Он доступен по следующему пути:</span><span class="sxs-lookup"><span data-stu-id="95442-111">It is available from the following path:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="95442-112">Upload **tab.zip** **App Studio**.</span><span class="sxs-lookup"><span data-stu-id="95442-112">Upload **tab.zip** to **App Studio**.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="95442-113">Обновление пакета приложений с помощью редактора Manifest</span><span class="sxs-lookup"><span data-stu-id="95442-113">Update your app package with Manifest editor</span></span>

<span data-ttu-id="95442-114">После отправки пакета приложений в App Studio необходимо настроить его.</span><span class="sxs-lookup"><span data-stu-id="95442-114">After you have uploaded your app package into App Studio, you must configure it.</span></span>

<span data-ttu-id="95442-115">Выберите плитку для недавно импортируемой вкладки в правой панели приветствия редактора Манифеста.</span><span class="sxs-lookup"><span data-stu-id="95442-115">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="95442-116">В левой части редактора Манифеста имеется список действий, а справа — список свойств, которые должны иметь значения для каждого из этих действий.</span><span class="sxs-lookup"><span data-stu-id="95442-116">There is a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="95442-117">Большая часть сведений предоставлена вашими **manifest.js,** но есть поля, которые необходимо обновить.</span><span class="sxs-lookup"><span data-stu-id="95442-117">Much of the information has been provided by your **manifest.json** but there are fields that you must update.</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="95442-118">Сведения: сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="95442-118">Details: App details</span></span>

<span data-ttu-id="95442-119">В разделе **Сведения о приложении:**</span><span class="sxs-lookup"><span data-stu-id="95442-119">In the **App details** section:</span></span>

1. <span data-ttu-id="95442-120">В **статье Идентификация** выберите **Создание** для создания нового удостоверения приложения для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="95442-120">Under **Identification**, select **Generate** to generate a new App Id for your app.</span></span>

1. <span data-ttu-id="95442-121">По **сведениям разработчика,** **обновите веб-сайт** **url-адресом https ngrok.**</span><span class="sxs-lookup"><span data-stu-id="95442-121">Under **Developer information**, update the **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="95442-122">В **URL-адресах** приложений обнови заявление **конфиденциальности** и условия использования `https://<yourngrokurl>/privacy` **для** `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="95442-122">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="95442-123">Возможности: Вкладки</span><span class="sxs-lookup"><span data-stu-id="95442-123">Capabilities: Tabs</span></span>

<span data-ttu-id="95442-124">В разделе **Tabs:**</span><span class="sxs-lookup"><span data-stu-id="95442-124">In the **Tabs** section:</span></span>

1. <span data-ttu-id="95442-125">В **статье Добавить личную вкладку** выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="95442-125">Under **Add a personal tab**, select **Add**.</span></span> <span data-ttu-id="95442-126">Появляется всплывающее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="95442-126">A pop-up dialog box appears.</span></span>

1. <span data-ttu-id="95442-127">Введите имя личной вкладки в **Name**.</span><span class="sxs-lookup"><span data-stu-id="95442-127">Enter a name for the personal tab in **Name**.</span></span>

1. <span data-ttu-id="95442-128">Введите **ID объекта**.</span><span class="sxs-lookup"><span data-stu-id="95442-128">Enter the **Entity ID**.</span></span>

1. <span data-ttu-id="95442-129">Обновление **URL-адреса** контента `https://<yourngrokurl>/personalTab` с помощью .</span><span class="sxs-lookup"><span data-stu-id="95442-129">Update **Content URL** with `https://<yourngrokurl>/personalTab`.</span></span>

    <span data-ttu-id="95442-130">Оставьте **поле URL-адрес веб-сайта** пустым.</span><span class="sxs-lookup"><span data-stu-id="95442-130">Leave the **Website URL** field blank.</span></span>

1. <span data-ttu-id="95442-131">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="95442-131">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="95442-132">Finish: Домены и разрешения</span><span class="sxs-lookup"><span data-stu-id="95442-132">Finish: Domains and permissions</span></span>

<span data-ttu-id="95442-133">В разделе **Домены и** разрешения  домены из поля вкладок должны содержать URL-адрес ngrok без префикса `<yourngrokurl>.ngrok.io/` HTTPS.</span><span class="sxs-lookup"><span data-stu-id="95442-133">In the **Domains and permissions** section, the **Domains from your tabs** field must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="95442-134">Finish: Test and distribute</span><span class="sxs-lookup"><span data-stu-id="95442-134">Finish: Test and distribute</span></span>

>[!IMPORTANT]
> <span data-ttu-id="95442-135">Справа в **описании** см. следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="95442-135">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="95442-136">&#9888; массив **"validDomains" не может содержать сайт тоннелей...**</span><span class="sxs-lookup"><span data-stu-id="95442-136">&#9888; **The 'validDomains' array cannot contain a tunneling site...**</span></span>
>
><span data-ttu-id="95442-137">Это предупреждение можно игнорировать при тестировании вкладки.</span><span class="sxs-lookup"><span data-stu-id="95442-137">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="95442-138">В разделе **Тест и распространение** выберите **Установите**.</span><span class="sxs-lookup"><span data-stu-id="95442-138">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="95442-139">В диалоговом окне всплывающее окно выберите **Добавить,** и вкладка отображается с двумя вариантами.</span><span class="sxs-lookup"><span data-stu-id="95442-139">In the pop-up dialog box, select **Add** and your tab is displayed with two options.</span></span>

1. <span data-ttu-id="95442-140">Из параметров на вкладке выберите **Выберите серый** или **выберите красный**.</span><span class="sxs-lookup"><span data-stu-id="95442-140">From the options in the tab, choose either **Select Gray** or **Select Red**.</span></span> <span data-ttu-id="95442-141">Вкладка отображается в соответствии с выбранным цветом.</span><span class="sxs-lookup"><span data-stu-id="95442-141">The tab is displayed according to the color you selected.</span></span>
 
    ![Личная вкладка ASPNETMVC, загруженная](../../assets/images/tab-images/personaltabaspnetmvcuploaded.png)

## <a name="view-your-personal-tab"></a><span data-ttu-id="95442-143">Просмотр личной вкладки</span><span class="sxs-lookup"><span data-stu-id="95442-143">View your personal tab</span></span>

1. <span data-ttu-id="95442-144">В панели навигации, расположенной слева от Teams, выберите &#x25CF;&#x25CF;&#x25CF;.</span><span class="sxs-lookup"><span data-stu-id="95442-144">In the navigation bar located at the far left of the Teams app, select the ellipses &#x25CF;&#x25CF;&#x25CF;.</span></span> <span data-ttu-id="95442-145">Показан список личных приложений.</span><span class="sxs-lookup"><span data-stu-id="95442-145">A list of personal apps is shown.</span></span>

1. <span data-ttu-id="95442-146">Выберите вкладку из списка, чтобы просмотреть ее.</span><span class="sxs-lookup"><span data-stu-id="95442-146">Select your tab from the list to view it.</span></span>
