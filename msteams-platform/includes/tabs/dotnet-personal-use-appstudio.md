## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="c40d9-101">Отправка вкладки в Teams с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="c40d9-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="c40d9-102">Мы используем приложение App Studio, чтобы изменить файл **manifest. JSON** и отправить завершенный пакет в Teams.</span><span class="sxs-lookup"><span data-stu-id="c40d9-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="c40d9-103">Вы также можете вручную изменить **манифест. JSON** , если хотите.</span><span class="sxs-lookup"><span data-stu-id="c40d9-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="c40d9-104">Если вы сделаете это, не забудьте создать решение еще раз, чтобы создать ZIP-файл **Tab** для отправки.</span><span class="sxs-lookup"><span data-stu-id="c40d9-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="c40d9-105">Откройте клиент Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c40d9-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="c40d9-106">Если вы используете [версию на основе веб-сайта](https://teams.microsoft.com) , вы можете проверить интерфейсный код с помощью [средств разработчика](~/tabs/how-to/developer-tools.md)в браузере.</span><span class="sxs-lookup"><span data-stu-id="c40d9-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="c40d9-107">Откройте приложение App Studio и выберите вкладку **редактор манифестов** .</span><span class="sxs-lookup"><span data-stu-id="c40d9-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="c40d9-108">В редакторе манифеста выберите **импортировать существующую** плитку приложения, чтобы начать обновление пакета приложения для вкладки. Исходный код сопровождается собственным частично завершенным манифестом.</span><span class="sxs-lookup"><span data-stu-id="c40d9-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="c40d9-109">Имя пакета приложения — **TAB. zip**.</span><span class="sxs-lookup"><span data-stu-id="c40d9-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="c40d9-110">Его можно найти здесь:</span><span class="sxs-lookup"><span data-stu-id="c40d9-110">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/Tab.zip
```

- <span data-ttu-id="c40d9-111">Отправка **вкладки** в App Studio. zip.</span><span class="sxs-lookup"><span data-stu-id="c40d9-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="c40d9-112">Обновление пакета приложения с помощью редактора манифеста</span><span class="sxs-lookup"><span data-stu-id="c40d9-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="c40d9-113">После того как вы отправили пакет приложений в приложение App Studio, вам потребуется завершить его настройку.</span><span class="sxs-lookup"><span data-stu-id="c40d9-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="c40d9-114">На правой панели страницы приветствия редактора манифеста выберите плитку для вновь импортированной вкладки.</span><span class="sxs-lookup"><span data-stu-id="c40d9-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="c40d9-115">В левой части редактора манифеста есть список действий, а справа — список свойств, значения которых должны быть заданы для каждого из этих шагов.</span><span class="sxs-lookup"><span data-stu-id="c40d9-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="c40d9-116">Многие из этих сведений предоставлены в файле *manifest. JSON* , но существует несколько полей, которые необходимо обновить:</span><span class="sxs-lookup"><span data-stu-id="c40d9-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="c40d9-117">Сведения: сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="c40d9-117">Details: App details</span></span>

<span data-ttu-id="c40d9-118">В разделе *сведения о приложении* :</span><span class="sxs-lookup"><span data-stu-id="c40d9-118">In the *App details* section:</span></span>

- <span data-ttu-id="c40d9-119">В разделе *Идентификация* нажмите **создать** , чтобы создать новый идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="c40d9-119">Under *Identification* select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="c40d9-120">В разделе *сведения для разработчиков* обновите URL- **адрес веб-сайта** с помощью URL-адреса *ngrok* HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c40d9-120">Under *Developer information* update the **Website URL** with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="c40d9-121">В *разделе URL-адреса приложений* обновите `https://<yourngrokurl>/privacy` заявление **о конфиденциальности** и условия `https://<yourngrokurl>/tou` его **использования** для>.</span><span class="sxs-lookup"><span data-stu-id="c40d9-121">Under *App URLs* update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="c40d9-122">Возможности: вкладки</span><span class="sxs-lookup"><span data-stu-id="c40d9-122">Capabilities: Tabs</span></span>

<span data-ttu-id="c40d9-123">В разделе *вкладки* :</span><span class="sxs-lookup"><span data-stu-id="c40d9-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="c40d9-124">В разделе *Добавление личной вкладки* нажмите кнопку ***Добавить***.</span><span class="sxs-lookup"><span data-stu-id="c40d9-124">Under *Add a personal tab* select ***Add***.</span></span> <span data-ttu-id="c40d9-125">Откроется всплывающее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="c40d9-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="c40d9-126">Заполните поле *имя* .</span><span class="sxs-lookup"><span data-stu-id="c40d9-126">Complete the *Name* field.</span></span>

- <span data-ttu-id="c40d9-127">Заполните поле " *идентификатор сущности* ".</span><span class="sxs-lookup"><span data-stu-id="c40d9-127">Complete the *Entity Id* field.</span></span>

- <span data-ttu-id="c40d9-128">Обновите поле *URL-адрес содержимого* с помощью `https://<yourngrokurl>/personalTab`.</span><span class="sxs-lookup"><span data-stu-id="c40d9-128">Update the *Content URL* field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="c40d9-129">Оставьте поле *URL-адрес веб-сайта* пустым.</span><span class="sxs-lookup"><span data-stu-id="c40d9-129">Leave the *Website URL* field blank.</span></span>

- <span data-ttu-id="c40d9-130">Нажмите кнопку ***Сохранить***.</span><span class="sxs-lookup"><span data-stu-id="c40d9-130">Select ***Save***.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="c40d9-131">Готово: домены и разрешения</span><span class="sxs-lookup"><span data-stu-id="c40d9-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="c40d9-132">В разделе *домены и разрешения* *домены из поля вкладки* должны содержать URL-адрес NGROK без префикса HTTPS `<yourngrokurl>.ngrok.io/`.</span><span class="sxs-lookup"><span data-stu-id="c40d9-132">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="c40d9-133">Готово: тестирование и распределение</span><span class="sxs-lookup"><span data-stu-id="c40d9-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="c40d9-134">В поле **Описание** справа появится следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="c40d9-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="c40d9-135">&#9888; "**массив" валиддомаинс "не может содержать туннельный сайт...**"</span><span class="sxs-lookup"><span data-stu-id="c40d9-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="c40d9-136">Это предупреждение можно игнорировать при тестировании вкладки.</span><span class="sxs-lookup"><span data-stu-id="c40d9-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="c40d9-137">В разделе " *тестирование и распространение* ":</span><span class="sxs-lookup"><span data-stu-id="c40d9-137">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="c40d9-138">Нажать кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="c40d9-138">Select **Install**.</span></span>

- <span data-ttu-id="c40d9-139">Во всплывающем окне убедитесь, что *для параметра Добавить для вас* задано значение *Да* , а для *команды Добавить в группу или чат* задано значение *нет*.</span><span class="sxs-lookup"><span data-stu-id="c40d9-139">In the pop-up window make sure that *Add for you* is set to *Yes* and *Add to a team or chat* is set to *No*.</span></span>

- <span data-ttu-id="c40d9-140">Нажать кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="c40d9-140">Select **Install**.</span></span>

- <span data-ttu-id="c40d9-141">В следующем всплывающем окне выберите **Открыть** , и вкладка отобразится.</span><span class="sxs-lookup"><span data-stu-id="c40d9-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="c40d9-142">Просмотр личной вкладки</span><span class="sxs-lookup"><span data-stu-id="c40d9-142">View your personal tab</span></span>

- <span data-ttu-id="c40d9-143">В области навигации, расположенной в левом углу приложения Teams, выберите `...` меню.</span><span class="sxs-lookup"><span data-stu-id="c40d9-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="c40d9-144">Вы увидите список личных приложений.</span><span class="sxs-lookup"><span data-stu-id="c40d9-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="c40d9-145">Выберите вкладку в списке, чтобы просмотреть его.</span><span class="sxs-lookup"><span data-stu-id="c40d9-145">Select your tab from the list to view.</span></span>
