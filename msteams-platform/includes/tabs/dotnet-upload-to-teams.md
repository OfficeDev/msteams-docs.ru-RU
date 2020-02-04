## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="2a37b-101">Отправка вкладки в Teams с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="2a37b-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="2a37b-102">Мы используем приложение App Studio, чтобы изменить файл **manifest. JSON** и отправить завершенный пакет в Teams.</span><span class="sxs-lookup"><span data-stu-id="2a37b-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="2a37b-103">Вы также можете вручную изменить файл **manifest. JSON** , если вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="2a37b-103">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="2a37b-104">Если вы сделаете это, не забудьте создать решение еще раз, чтобы создать ZIP-файл **Tab** для отправки.</span><span class="sxs-lookup"><span data-stu-id="2a37b-104">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="2a37b-105">Откройте клиент Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2a37b-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="2a37b-106">Если вы используете [версию на основе веб-сайта](https://teams.microsoft.com) , вы можете проверить интерфейсный код с помощью [средств разработчика](~/tabs/how-to/developer-tools.md)в браузере.</span><span class="sxs-lookup"><span data-stu-id="2a37b-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="2a37b-107">Откройте приложение App Studio и выберите вкладку **редактор манифестов** .</span><span class="sxs-lookup"><span data-stu-id="2a37b-107">Open the App Studio app and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="2a37b-108">В редакторе манифеста выберите **импортировать существующую** плитку приложения, чтобы начать обновление пакета приложения для вкладки. Исходный код сопровождается собственным частично завершенным манифестом.</span><span class="sxs-lookup"><span data-stu-id="2a37b-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="2a37b-109">Имя пакета приложения — **TAB. zip**.</span><span class="sxs-lookup"><span data-stu-id="2a37b-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="2a37b-110">Его можно найти здесь:</span><span class="sxs-lookup"><span data-stu-id="2a37b-110">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- <span data-ttu-id="2a37b-111">Отправка **вкладки** в App Studio. zip.</span><span class="sxs-lookup"><span data-stu-id="2a37b-111">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="2a37b-112">Обновление пакета приложения с помощью редактора манифеста</span><span class="sxs-lookup"><span data-stu-id="2a37b-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="2a37b-113">После того как вы отправили пакет приложений в приложение App Studio, вам потребуется завершить его настройку.</span><span class="sxs-lookup"><span data-stu-id="2a37b-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="2a37b-114">На правой панели страницы приветствия редактора манифеста выберите плитку для вновь импортированной вкладки.</span><span class="sxs-lookup"><span data-stu-id="2a37b-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="2a37b-115">В левой части редактора манифеста есть список действий, а справа — список свойств, значения которых должны быть заданы для каждого из этих шагов.</span><span class="sxs-lookup"><span data-stu-id="2a37b-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="2a37b-116">Многие из этих сведений предоставлены в файле *manifest. JSON* , но существует несколько полей, которые необходимо обновить:</span><span class="sxs-lookup"><span data-stu-id="2a37b-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="2a37b-117">Сведения: сведения о приложении</span><span class="sxs-lookup"><span data-stu-id="2a37b-117">Details: App details</span></span>

- <span data-ttu-id="2a37b-118">В разделе *Идентификация* нажмите **создать** , чтобы создать новый идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="2a37b-118">Under *Identification* select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="2a37b-119">В разделе *сведения для разработчиков* обновите поле URL- **адрес веб-сайта** с помощью URL-адреса *ngrok* HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2a37b-119">Under *Developer information* update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="2a37b-120">В *разделе URL-адреса приложений* обновите `https://<yourngrokurl>/privacy` заявление **о конфиденциальности** и условия `https://<yourngrokurl>/tou` его **использования** для>.</span><span class="sxs-lookup"><span data-stu-id="2a37b-120">Under *App URLs* update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="2a37b-121">Возможности: вкладки</span><span class="sxs-lookup"><span data-stu-id="2a37b-121">Capabilities: Tabs</span></span>

<span data-ttu-id="2a37b-122">В разделе *вкладки* :</span><span class="sxs-lookup"><span data-stu-id="2a37b-122">In the *Tabs* section:</span></span>

- <span data-ttu-id="2a37b-123">На *вкладке Группа* нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2a37b-123">Under *Team Tab* select **Add**.</span></span>

- <span data-ttu-id="2a37b-124">Во всплывающем окне вкладки команды обновите *URL-адрес конфигурации* до `https://<yourngrokurl>/tab`.</span><span class="sxs-lookup"><span data-stu-id="2a37b-124">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="2a37b-125">И, наконец, убедитесь, что вы *можете обновить конфигурацию? Флажки группа и* *Групповая беседа* отмечены и нажмите кнопку **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2a37b-125">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="2a37b-126">Готово: домены и разрешения</span><span class="sxs-lookup"><span data-stu-id="2a37b-126">Finish: Domains and permissions</span></span>

<span data-ttu-id="2a37b-127">В разделе *домены и разрешения* *домены из поля вкладки* должны содержать URL-адрес NGROK без префикса HTTPS `<yourngrokurl>.ngrok.io/`.</span><span class="sxs-lookup"><span data-stu-id="2a37b-127">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="2a37b-128">Готово: тестирование и распределение</span><span class="sxs-lookup"><span data-stu-id="2a37b-128">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="2a37b-129">В поле **Описание** справа появится следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="2a37b-129">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="2a37b-130">&#9888; "**массив" валиддомаинс "не может содержать туннельный сайт...**"</span><span class="sxs-lookup"><span data-stu-id="2a37b-130">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="2a37b-131">Это предупреждение можно игнорировать при тестировании вкладки.</span><span class="sxs-lookup"><span data-stu-id="2a37b-131">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="2a37b-132">В разделе " *тестирование и распространение* ":</span><span class="sxs-lookup"><span data-stu-id="2a37b-132">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="2a37b-133">Нажать кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="2a37b-133">Select **Install**.</span></span>

- <span data-ttu-id="2a37b-134">Во всплывающем окне *Добавление в группу или в* поле "разговор" введите команду и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="2a37b-134">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="2a37b-135">В следующем всплывающем окне выберите канал команды, в котором будет отображаться вкладка, и нажмите кнопку **настроить**.</span><span class="sxs-lookup"><span data-stu-id="2a37b-135">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="2a37b-136">В последнем всплывающем окне выберите значение для вкладки (красный или серый значок) и нажмите кнопку **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2a37b-136">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="2a37b-137">Чтобы просмотреть вкладку, перейдите к группе, в которой она была установлена, и выберите ее в панели вкладок.</span><span class="sxs-lookup"><span data-stu-id="2a37b-137">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="2a37b-138">Должна отобразиться страница, выбранная во время настройки.</span><span class="sxs-lookup"><span data-stu-id="2a37b-138">The page that you chose during configuration should be displayed.</span></span>
