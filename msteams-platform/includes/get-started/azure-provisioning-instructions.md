## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="9ac7c-101">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="9ac7c-101">Deploy your app to Azure</span></span>

<span data-ttu-id="9ac7c-102">Развертывание состоит из двух этапов.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-102">Deployment consists of two steps.</span></span>  <span data-ttu-id="9ac7c-103">Сначала создаются необходимые облачные ресурсы (также известные как подготовка), затем код, который составляет ваше приложение, копируется в созданные облачные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-103">First, necessary cloud resources are created (also known as provisioning), then the code that makes up your app is copied into the created cloud resources.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="9ac7c-104">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9ac7c-104">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="9ac7c-105">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-105">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="9ac7c-106">Выберите Teams набор средств на боковой панели, выбрав значок Teams.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-106">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="9ac7c-107">Выберите **Положение в облаке**.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-107">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Снимок экрана, показывающий команды по подготовкам":::

1. <span data-ttu-id="9ac7c-109">При необходимости выберите подписку для использования для ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-109">If required, select a subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9ac7c-110">Для размещения приложения всегда используются некоторые ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-110">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="9ac7c-111">Диалоговое окно предупреждает, что при запуске ресурсов в Azure могут возникнуть затраты.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-111">A dialog warns you that costs may be incurred when running resources in Azure.</span></span>  <span data-ttu-id="9ac7c-112">Press **Provision**.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-112">Press **Provision**.</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-warning.png" alt-text="Снимок экрана диалогового временного набора.":::

   <span data-ttu-id="9ac7c-114">Процесс подготовка создаст ресурсы в облаке Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-114">The provisioning process will create resources in the Azure cloud.</span></span>  <span data-ttu-id="9ac7c-115">Это займет некоторое время.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-115">This will take some time.</span></span>  <span data-ttu-id="9ac7c-116">Вы можете отслеживать ход, наблюдая за диалогами в правом нижнем углу.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-116">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="9ac7c-117">Через несколько минут вы увидите следующее уведомление:</span><span class="sxs-lookup"><span data-stu-id="9ac7c-117">After a few minutes, you will see the following notice:</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Снимок экрана, показывающий полный диалоговое окно подготовка.":::

1. <span data-ttu-id="9ac7c-119">Как только подготовка завершена, выберите **Развертывание в облаке.**</span><span class="sxs-lookup"><span data-stu-id="9ac7c-119">Once provisioning is complete, select **Deploy to the Cloud**.</span></span>  <span data-ttu-id="9ac7c-120">Как и в случае с подготовками, этот процесс занимает некоторое время.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-120">As with provisioning, this process takes some time.</span></span>  <span data-ttu-id="9ac7c-121">Вы можете отслеживать процесс, наблюдая диалоги в правом нижнем углу.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-121">You can monitor the process by watching the dialogs in the bottom right corner.</span></span> <span data-ttu-id="9ac7c-122">Через несколько минут вы увидите уведомление о завершении.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-122">After a few minutes, you will see a completion notice.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="9ac7c-123">Командная строка</span><span class="sxs-lookup"><span data-stu-id="9ac7c-123">Command Line</span></span>](#tab/cli)

<span data-ttu-id="9ac7c-124">В окне терминала:</span><span class="sxs-lookup"><span data-stu-id="9ac7c-124">In your terminal window:</span></span>

1. <span data-ttu-id="9ac7c-125">Запуск `teamsfx provision` .</span><span class="sxs-lookup"><span data-stu-id="9ac7c-125">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="9ac7c-126">Возможно, вам будет предложено войти в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-126">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="9ac7c-127">При необходимости вам будет предложено выбрать подписку Azure для использования для ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-127">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9ac7c-128">Для размещения приложения всегда используются некоторые ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-128">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="9ac7c-129">Запуск `teamsfx deploy` .</span><span class="sxs-lookup"><span data-stu-id="9ac7c-129">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> <span data-ttu-id="9ac7c-130">**В чем разница между Provision и Deploy?**</span><span class="sxs-lookup"><span data-stu-id="9ac7c-130">**What's the difference between Provision and Deploy?**</span></span>
>
> <span data-ttu-id="9ac7c-131">На **шаге Provision** будут создаваться ресурсы в Azure и M365 для вашего приложения, но код (HTML, CSS, JavaScript и т.д.) не копируется в ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-131">The **Provision** step will create resources in Azure and M365 for your app, but no code (HTML, CSS, JavaScript, etc.) is copied to the resources.</span></span>  <span data-ttu-id="9ac7c-132">Шаг **Deploy** скопирует код приложения на ресурсы, созданные во время шага по предоставлению.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-132">The **Deploy** step will copy the code for your app to the resources you created during the provision step.</span></span>  <span data-ttu-id="9ac7c-133">Часто развертывается несколько раз без предоставления новых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-133">It is common to deploy multiple times without provisioning new resources.</span></span> <span data-ttu-id="9ac7c-134">Так как этап предоставления может занять некоторое время, он отделен от шага развертывания.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-134">Since the provision step can take some time to complete, it is separate from the deployment step.</span></span>

<span data-ttu-id="9ac7c-135">После завершения этапов подготовка и развертывание:</span><span class="sxs-lookup"><span data-stu-id="9ac7c-135">Once the provisioning and deployment steps are finished:</span></span>

1. <span data-ttu-id="9ac7c-136">С Visual Studio Code откройте панель отключки **(Ctrl+Shift+D**  /  **⌘⇧-D** или **Просмотр > Run**)</span><span class="sxs-lookup"><span data-stu-id="9ac7c-136">From Visual Studio Code, open the debug panel (**Ctrl+Shift+D** / **⌘⇧-D** or **View > Run**)</span></span>
1. <span data-ttu-id="9ac7c-137">Выберите **Пульт запуска (Edge)** из выпадаемой конфигурации запуска.</span><span class="sxs-lookup"><span data-stu-id="9ac7c-137">Select **Launch Remote (Edge)** from the launch configuration drop-down.</span></span>
1. <span data-ttu-id="9ac7c-138">Нажмите кнопку Play, чтобы запустить приложение — теперь он работает удаленно из Azure!</span><span class="sxs-lookup"><span data-stu-id="9ac7c-138">Press the Play button to launch your app - now running remotely from Azure!</span></span>
