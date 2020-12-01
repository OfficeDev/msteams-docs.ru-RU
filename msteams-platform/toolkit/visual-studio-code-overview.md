---
title: Создание приложений с помощью набора инструментов Microsoft Teams и кода Visual Studio
description: Приступая к созданию привлекательных пользовательских приложений непосредственно в Visual Studio Code с помощью набора инструментов Microsoft Teams
keywords: набор средств Visual Studio Code Toolkit для Teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 41b0eeaeef1c7094fc9c8cbdc05c2db899245fc6
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/30/2020
ms.locfileid: "49476932"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="f1e93-104">Создание приложений с помощью набора инструментов Teams и кода Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f1e93-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="f1e93-105">Набор средств Microsoft Teams позволяет создавать пользовательские приложения Teams непосредственно в среде Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f1e93-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="f1e93-106">Набор средств поможет вам выполнить все действия, необходимые для создания, отладки и запуска приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="f1e93-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="f1e93-107">Установка набора инструментов Teams</span><span class="sxs-lookup"><span data-stu-id="f1e93-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="f1e93-108">Набор средств Microsoft Teams для Visual Studio Code доступен для загрузки с [Visual Studio Marketplace](https://aka.ms/teams-toolkit) или напрямую в виде расширения в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f1e93-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="f1e93-109">После установки вы должны увидеть набор инструментов Teams на панели действий Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f1e93-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="f1e93-110">Если это не так, щелкните правой кнопкой мыши на панели действий и выберите **Microsoft Teams** , чтобы закрепить набор инструментов для упрощения доступа.</span><span class="sxs-lookup"><span data-stu-id="f1e93-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="f1e93-111">Использование набора средств</span><span class="sxs-lookup"><span data-stu-id="f1e93-111">Using the toolkit</span></span>

- [<span data-ttu-id="f1e93-112">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="f1e93-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="f1e93-113">Импорт существующего проекта</span><span class="sxs-lookup"><span data-stu-id="f1e93-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="f1e93-114">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="f1e93-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="f1e93-115">Упаковка приложения</span><span class="sxs-lookup"><span data-stu-id="f1e93-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="f1e93-116">Запуск приложения на локальном компьютере или в Teams</span><span class="sxs-lookup"><span data-stu-id="f1e93-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="f1e93-117">Настройка нового проекта Teams</span><span class="sxs-lookup"><span data-stu-id="f1e93-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="f1e93-118">Создайте рабочую область или папку для проекта в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="f1e93-118">Create a workspace/folder for your project in your local environment.</span></span>
1. <span data-ttu-id="f1e93-119">В Visual Studio Code выберите значок команды</span><span class="sxs-lookup"><span data-stu-id="f1e93-119">In Visual Studio Code, select the Teams icon</span></span> ![Значок Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="f1e93-121">на панели действий в левой части окна.</span><span class="sxs-lookup"><span data-stu-id="f1e93-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="f1e93-122">Выберите **Открыть набор инструментов Microsoft Teams** в меню команд.</span><span class="sxs-lookup"><span data-stu-id="f1e93-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="f1e93-123">Выберите **создать приложение Teams** из меню команд.</span><span class="sxs-lookup"><span data-stu-id="f1e93-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="f1e93-124">При появлении соответствующего запроса введите имя рабочей области.</span><span class="sxs-lookup"><span data-stu-id="f1e93-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="f1e93-125">Он будет использоваться в качестве имени папки, в которой будет размещаться проект, и именем приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f1e93-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="f1e93-126">Нажмите клавишу **Ввод** , и вы будете доставлены на экране **добавить возможности** настройте свойства нового приложения.</span><span class="sxs-lookup"><span data-stu-id="f1e93-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="f1e93-127">Нажмите кнопку **Готово** , чтобы завершить процесс настройки.</span><span class="sxs-lookup"><span data-stu-id="f1e93-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="f1e93-128">Импорт существующего проекта приложения Teams</span><span class="sxs-lookup"><span data-stu-id="f1e93-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="f1e93-129">В Visual Studio Code выберите значок команды</span><span class="sxs-lookup"><span data-stu-id="f1e93-129">In Visual Studio Code, select the Teams icon</span></span> ![Значок Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="f1e93-131">на панели действий в левой части окна.</span><span class="sxs-lookup"><span data-stu-id="f1e93-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="f1e93-132">Выберите пункт **Импорт пакета приложения** в меню команда.</span><span class="sxs-lookup"><span data-stu-id="f1e93-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="f1e93-133">Выберите существующий ZIP-файл [пакета приложения Teams](../concepts/build-and-test/apps-package.md) .</span><span class="sxs-lookup"><span data-stu-id="f1e93-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="f1e93-134">Нажмите кнопку **выбрать пакет публикации** .</span><span class="sxs-lookup"><span data-stu-id="f1e93-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="f1e93-135">Теперь на вкладке Конфигурация набора средств необходимо заполнить сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="f1e93-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="f1e93-136">В Visual Studio Code выберите **файл**  ->  **Добавить папку в рабочую область** , чтобы добавить каталог с исходным кодом в рабочую область Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f1e93-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="f1e93-137">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="f1e93-137">Configure your app</span></span>

<span data-ttu-id="f1e93-138">В основном приложение Teams поработает с тремя компонентами:</span><span class="sxs-lookup"><span data-stu-id="f1e93-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="f1e93-139">Клиент Microsoft Teams (веб-сайт, Настольный компьютер или мобильное устройство), на котором пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="f1e93-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="f1e93-140">Сервер, который отвечает на запросы для контента, который будет отображаться в Teams, например, контент вкладки HTML или адаптивной карточки Bot.</span><span class="sxs-lookup"><span data-stu-id="f1e93-140">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="f1e93-141">[Пакет приложения](/concepts/build-and-test/apps-package.md) Teams состоит из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="f1e93-141">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="f1e93-142">manifest.jsна</span><span class="sxs-lookup"><span data-stu-id="f1e93-142">The manifest.json</span></span> 
  > - <span data-ttu-id="f1e93-143">[Значок цвета](../resources/schema/manifest-schema.md#icons) приложения для отображения в каталоге приложений "общедоступный" или "Организация"</span><span class="sxs-lookup"><span data-stu-id="f1e93-143">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="f1e93-144">[Значок структуры](../resources/schema/manifest-schema.md#icons) для отображения на панели активности Teams.</span><span class="sxs-lookup"><span data-stu-id="f1e93-144">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="f1e93-145">При установке приложения клиент Teams анализирует файл манифеста, чтобы определить необходимые сведения, такие как имя вашего приложения и URL-адрес, по которому расположены службы.</span><span class="sxs-lookup"><span data-stu-id="f1e93-145">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="f1e93-146">Чтобы настроить приложение, перейдите на вкладку **набор инструментов Microsoft Teams** в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f1e93-146">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="f1e93-147">Выберите команду **изменить пакет приложения** , чтобы просмотреть страницу **сведений о приложении** .</span><span class="sxs-lookup"><span data-stu-id="f1e93-147">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="f1e93-148">Изменение полей на странице "сведения о приложении" обновляет содержимое manifest.jsв файле, который в конечном итоге будет поставляться в составе пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="f1e93-148">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="f1e93-149">*Просмотр* [редактора манифестов App Studio](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="f1e93-149">*See* [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="f1e93-150">Упаковка приложения</span><span class="sxs-lookup"><span data-stu-id="f1e93-150">Package your app</span></span>

<span data-ttu-id="f1e93-151">Изменение страницы **сведений о приложении** или обновление **манифеста** или файлов **env** в папке  **публикации** приложения автоматически создаст файл **Development.zip** .</span><span class="sxs-lookup"><span data-stu-id="f1e93-151">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="f1e93-152">Необходимо включить [два значка](../concepts/build-and-test/apps-package.md#icons) в одну и ту же папку.</span><span class="sxs-lookup"><span data-stu-id="f1e93-152">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#icons) in that same folder.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="f1e93-153">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1e93-153">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="f1e93-154">Установка и запуск приложения на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="f1e93-154">Install and run your app locally</span></span>

<span data-ttu-id="f1e93-155">Для получения подробных инструкций по упаковке и тестированию приложения обратитесь к главной странице "\**Построение и запуск* контента в проекте".</span><span class="sxs-lookup"><span data-stu-id="f1e93-155">Refer to the \**Build and Run* content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="f1e93-156">В общем случае необходимо установить сервер приложения, заставить его работать, а затем настроить туннельное решение, чтобы Teams могла получить доступ к содержимому, запущенному с localhost.</span><span class="sxs-lookup"><span data-stu-id="f1e93-156">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="f1e93-157">Включение разработки с localhost</span><span class="sxs-lookup"><span data-stu-id="f1e93-157">Enable development from localhost</span></span>

<span data-ttu-id="f1e93-158">Если вы хотите выполнить отладку приложения на основе вкладки на localhost с использованием HTTPS, необходимо сообщить браузеру о доверии к приложению, с которого выполняется обращение <https://localhost> .</span><span class="sxs-lookup"><span data-stu-id="f1e93-158">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="f1e93-159">Перейдите по адресу <https://localhost:3000/tab>.</span><span class="sxs-lookup"><span data-stu-id="f1e93-159">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="f1e93-160">Если отображается предупреждение о том, что сайт не является доверенным, выберите параметр для продолжения.</span><span class="sxs-lookup"><span data-stu-id="f1e93-160">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="f1e93-161">Теперь ваше приложение должно быть доступно из клиента Teams.</span><span class="sxs-lookup"><span data-stu-id="f1e93-161">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="f1e93-162">Запуск приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="f1e93-162">Run your app in Teams</span></span>

<span data-ttu-id="f1e93-163">Предварительные требования: [Включение режима предварительного просмотра для разработчиков Teams](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="f1e93-163">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="f1e93-164">Перейдите на панель действий в левой части окна кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1e93-164">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="f1e93-165">Выберите значок **Run (выполнить** ) для отображения представления " **Запуск" и "Отладка** ".</span><span class="sxs-lookup"><span data-stu-id="f1e93-165">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="f1e93-166">Вы также можете использовать сочетание клавиш `Ctrl+Shift+D` .</span><span class="sxs-lookup"><span data-stu-id="f1e93-166">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1e93-167">Следующий шаг: обслуживание и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="f1e93-167">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
