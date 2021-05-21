---
title: Создание приложений с помощью Microsoft Teams набор средств и Visual Studio Code
description: Начало создания больших пользовательских приложений непосредственно Visual Studio Code с Microsoft Teams набор средств
keywords: команда визуальный набор кода студии
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: efd0962e9c4c0d64dbac47caf29b2e56907937b3
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566560"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="722ec-104">Создание приложений с помощью Teams набор средств и Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="722ec-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="722ec-105">Набор средств Microsoft Teams Toolkit позволяет создавать пользовательские приложения Teams непосредственно в среде Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="722ec-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="722ec-106">Этот набор средств предоставит вам пошаговые инструкции в процессе создания приложения, а также все необходимое для сборки, отладки и запуска вашего приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="722ec-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="722ec-107">Установка Teams набор средств</span><span class="sxs-lookup"><span data-stu-id="722ec-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="722ec-108">Приложение Microsoft Teams набор средств для Visual Studio Code доступно для скачивания с [Visual Studio Marketplace](https://aka.ms/teams-toolkit) или непосредственно в качестве расширения в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="722ec-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="722ec-109">После установки следует увидеть Teams набор средств в панели Visual Studio Code действий.</span><span class="sxs-lookup"><span data-stu-id="722ec-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="722ec-110">Если нет, щелкните правой кнопкой  мыши в панели действий и выберите Microsoft Teams, чтобы закрепить набор инструментов для легкого доступа.</span><span class="sxs-lookup"><span data-stu-id="722ec-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="722ec-111">Использование инструментария</span><span class="sxs-lookup"><span data-stu-id="722ec-111">Using the toolkit</span></span>

- [<span data-ttu-id="722ec-112">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="722ec-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="722ec-113">Импорт существующего проекта</span><span class="sxs-lookup"><span data-stu-id="722ec-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="722ec-114">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="722ec-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="722ec-115">Пакет приложения</span><span class="sxs-lookup"><span data-stu-id="722ec-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="722ec-116">Запустите приложение локально или в Teams</span><span class="sxs-lookup"><span data-stu-id="722ec-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="722ec-117">Настройка нового проекта Teams</span><span class="sxs-lookup"><span data-stu-id="722ec-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="722ec-118">Создайте рабочее пространство или папку для проекта в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="722ec-118">Create a workspace or folder for your project in your local environment.</span></span>
1. <span data-ttu-id="722ec-119">В Visual Studio Code выберите значок Teams</span><span class="sxs-lookup"><span data-stu-id="722ec-119">In Visual Studio Code, select the Teams icon</span></span> ![Значок Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="722ec-121">из панели действий в левой части окна.</span><span class="sxs-lookup"><span data-stu-id="722ec-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="722ec-122">Выберите **Откройте Microsoft Teams набор средств** из меню команды.</span><span class="sxs-lookup"><span data-stu-id="722ec-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="722ec-123">Выберите **Создание нового приложения Teams из** меню команды.</span><span class="sxs-lookup"><span data-stu-id="722ec-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="722ec-124">При запросе введите имя рабочего пространства.</span><span class="sxs-lookup"><span data-stu-id="722ec-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="722ec-125">Это будет использоваться как имя папки, в которой будет находиться ваш проект, так и имя приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="722ec-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="722ec-126">Нажмите **кнопку Ввод,** и вы прибудете на экран **Добавить возможности** настроить свойства для нового приложения.</span><span class="sxs-lookup"><span data-stu-id="722ec-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="722ec-127">Выберите **кнопку Готово,** чтобы завершить процесс настройки.</span><span class="sxs-lookup"><span data-stu-id="722ec-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="722ec-128">Импорт существующего проекта Teams приложений</span><span class="sxs-lookup"><span data-stu-id="722ec-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="722ec-129">В Visual Studio Code выберите значок Teams</span><span class="sxs-lookup"><span data-stu-id="722ec-129">In Visual Studio Code, select the Teams icon</span></span> ![Значок Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="722ec-131">из панели действий в левой части окна.</span><span class="sxs-lookup"><span data-stu-id="722ec-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="722ec-132">Выберите **пакет импортных приложений** из меню команды.</span><span class="sxs-lookup"><span data-stu-id="722ec-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="722ec-133">Выберите существующий [Teams почтовый файл пакета](../concepts/build-and-test/apps-package.md) приложений.</span><span class="sxs-lookup"><span data-stu-id="722ec-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="722ec-134">Выберите **кнопку Выбор пакета публикации.**</span><span class="sxs-lookup"><span data-stu-id="722ec-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="722ec-135">Теперь вкладка конфигурации инструментария должна заполняться сведениями о приложении.</span><span class="sxs-lookup"><span data-stu-id="722ec-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="722ec-136">В Visual Studio Code выберите **папку Добавить** файл в рабочее пространство, чтобы добавить каталог исходных кодов  ->   в Visual Studio Code рабочей области.</span><span class="sxs-lookup"><span data-stu-id="722ec-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="722ec-137">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="722ec-137">Configure your app</span></span>

<span data-ttu-id="722ec-138">В основе приложения Teams три компонента:</span><span class="sxs-lookup"><span data-stu-id="722ec-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="722ec-139">Клиент Microsoft Teams (веб-, настольный или мобильный), где пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="722ec-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="722ec-140">Сервер, который отвечает на запросы контента, который будет отображаться в Teams.</span><span class="sxs-lookup"><span data-stu-id="722ec-140">A server that responds to requests for content that will be displayed in Teams.</span></span> <span data-ttu-id="722ec-141">Например, содержимое htmL-вкладок или адаптивная карта бота.</span><span class="sxs-lookup"><span data-stu-id="722ec-141">For example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="722ec-142">Пакет [Teams, состоящий](/concepts/build-and-test/apps-package.md) из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="722ec-142">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="722ec-143">В manifest.js.</span><span class="sxs-lookup"><span data-stu-id="722ec-143">The manifest.json.</span></span> 
      > - <span data-ttu-id="722ec-144">Значок [цвета](../resources/schema/manifest-schema.md#icons) для отображения приложения в каталоге общедоступных или организаций.</span><span class="sxs-lookup"><span data-stu-id="722ec-144">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      > - <span data-ttu-id="722ec-145">Значок [плана](../resources/schema/manifest-schema.md#icons) для отображения на панели Teams действий.</span><span class="sxs-lookup"><span data-stu-id="722ec-145">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="722ec-146">При установке приложения клиент Teams определяет файл манифеста, чтобы определить необходимые сведения, такие как имя приложения и URL-адрес, в котором находятся службы.</span><span class="sxs-lookup"><span data-stu-id="722ec-146">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="722ec-147">Чтобы настроить приложение, перейдите на вкладку Microsoft Teams набор средств **в** Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="722ec-147">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="722ec-148">Выберите **пакет изменить приложение,** чтобы просмотреть **страницу сведений о приложении.**</span><span class="sxs-lookup"><span data-stu-id="722ec-148">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="722ec-149">Редактирование полей на странице сведения приложения обновляет содержимое manifest.jsфайла, который в конечном итоге будет отгрузка в составе пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="722ec-149">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="722ec-150">Дополнительные сведения см. в [редакторе манифеста App Studio](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="722ec-150">For more information, See [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="722ec-151">Пакет приложения</span><span class="sxs-lookup"><span data-stu-id="722ec-151">Package your app</span></span>

<span data-ttu-id="722ec-152">Изменение страницы **сведений** о **приложении,** манифеста или файлов env в **папке** **.publish** вашего приложения автоматически создает **Development.zip** файл.</span><span class="sxs-lookup"><span data-stu-id="722ec-152">Modifying the **app details** page, **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="722ec-153">В эту же [](../concepts/build-and-test/apps-package.md#app-icons) папку необходимо включить две значки.</span><span class="sxs-lookup"><span data-stu-id="722ec-153">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#app-icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="722ec-154">Установка и локальное запуск приложения</span><span class="sxs-lookup"><span data-stu-id="722ec-154">Install and run your app locally</span></span>

## <a name="run-your-app"></a><span data-ttu-id="722ec-155">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="722ec-155">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="722ec-156">Установка и локальное запуск приложения</span><span class="sxs-lookup"><span data-stu-id="722ec-156">Install and run your app locally</span></span>

<span data-ttu-id="722ec-157">Подробные инструкции по упаковке и проверке приложения можно найти на домашней странице проекта Build and **Run.**</span><span class="sxs-lookup"><span data-stu-id="722ec-157">Refer to the **Build and Run** content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="722ec-158">В общем, необходимо установить сервер приложения, его запуск, а затем настроить решение по Teams доступ к контенту из localhost.</span><span class="sxs-lookup"><span data-stu-id="722ec-158">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="722ec-159">Включить разработку из localhost</span><span class="sxs-lookup"><span data-stu-id="722ec-159">Enable development from localhost</span></span>

<span data-ttu-id="722ec-160">Если вы хотите отчудить приложение на основе вкладок на локальном канале с помощью HTTPS, вам потребуется сообщить браузеру, чтобы он доверял приложению, которое обслуживается из <https://localhost> .</span><span class="sxs-lookup"><span data-stu-id="722ec-160">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="722ec-161">Перейдите по адресу <https://localhost:3000/tab>.</span><span class="sxs-lookup"><span data-stu-id="722ec-161">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="722ec-162">Если вы видите предупреждение, указывающее на то, что сайту не доверяют, выберите вариант, чтобы продолжить работу в любом случае.</span><span class="sxs-lookup"><span data-stu-id="722ec-162">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="722ec-163">Теперь ваше приложение должно быть доступно Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="722ec-163">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="722ec-164">Запустите приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="722ec-164">Run your app in Teams</span></span>

<span data-ttu-id="722ec-165">Необходимые условия: [включить Teams режим предварительного просмотра разработчика](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="722ec-165">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="722ec-166">Перейдите к панели действий с левой стороны Visual Studio Code окна.</span><span class="sxs-lookup"><span data-stu-id="722ec-166">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="722ec-167">Выберите **значок Выполнить,** чтобы отобразить представление **Run и Debug.**</span><span class="sxs-lookup"><span data-stu-id="722ec-167">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="722ec-168">Вы также можете использовать ярлык клавиатуры `Ctrl+Shift+D` .</span><span class="sxs-lookup"><span data-stu-id="722ec-168">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

## <a name="next-step"></a><span data-ttu-id="722ec-169">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="722ec-169">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="722ec-170">Ведение и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="722ec-170">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
