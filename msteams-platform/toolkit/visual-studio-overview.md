---
title: Создание приложений с помощью Teams набор средств и Visual Studio
description: Начало создания больших пользовательских приложений непосредственно в Visual Studio с Microsoft Teams набор средств
keywords: набор инструментов для визуальной студии teams
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 996037f5bb1caaa2493e1eebe51039724822fef9
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949718"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="cb8dc-104">Создание приложений с помощью Teams набор средств и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb8dc-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="cb8dc-105">Набор средств Microsoft Teams Toolkit позволяет создавать пользовательские приложения Teams непосредственно в интегрированной среде разработки (IDE) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="cb8dc-106">Этот набор средств Microsoft Teams предоставит вам пошаговые инструкции в процессе создания приложения, а также все необходимое для сборки, отладки и запуска вашего приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb8dc-107">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="cb8dc-107">Prerequisites</span></span>

1. <span data-ttu-id="cb8dc-108">[Включить предварительный просмотр разработчика.](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)</span><span class="sxs-lookup"><span data-stu-id="cb8dc-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

1. <span data-ttu-id="cb8dc-109">Убедитесь, что **<span>ASP.NE</span>T** и модуль веб-разработки добавлены в экземпляр Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="cb8dc-110">Вы можете проверить, следуя шагам в изменении Visual Studio путем добавления или удаления рабочих нагрузок [и документации по компонентам.](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="cb8dc-110">You can check by following the steps in the [modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![Модуль visual studio asp.net](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="cb8dc-112">Если вы хотите проверить приложение, развернув его из Visual Studio, необходимо установить службы IIS (IIS)) в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-112">If you want to test your app by deploying it from Visual Studio, you must have Internet Information Services (IIS)) installed in your development environment.</span></span> <span data-ttu-id="cb8dc-113">Visual Studio не включает IIS и не входит в конфигурацию Windows 10, Windows 8 или Windows 7; Однако вы можете скачать последнюю версию из [центра загрузки Майкрософт.](https://www.microsoft.com/download/details.aspx?id=48264)</span><span class="sxs-lookup"><span data-stu-id="cb8dc-113">Visual Studio does not include IIS and it is not included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Представление страницы IIS для скачивания](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="cb8dc-115">Установка Teams набор средств</span><span class="sxs-lookup"><span data-stu-id="cb8dc-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="cb8dc-116">Приложение Microsoft Teams набор средств для Visual Studio доступно для скачивания с [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) или непосредственно  из меню Расширения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span> <span data-ttu-id="cb8dc-117">С Visual Studio Marketplace также [скачайте Teams набор средств для Visual Studio 2019](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit).</span><span class="sxs-lookup"><span data-stu-id="cb8dc-117">From the Visual Studio Marketplace also download [Teams Toolkit for Visual Studio 2019](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit).</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="cb8dc-118">Использование инструментария</span><span class="sxs-lookup"><span data-stu-id="cb8dc-118">Using the toolkit</span></span>

- [<span data-ttu-id="cb8dc-119">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="cb8dc-119">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="cb8dc-120">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="cb8dc-120">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="cb8dc-121">Пакет приложения</span><span class="sxs-lookup"><span data-stu-id="cb8dc-121">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="cb8dc-122">Установите и запустите приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="cb8dc-122">Install and run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="cb8dc-123">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="cb8dc-123">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="cb8dc-124">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="cb8dc-124">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="cb8dc-125">Настройка нового проекта Teams</span><span class="sxs-lookup"><span data-stu-id="cb8dc-125">Set up a new Teams project</span></span>

![Teams установлен набор инструментов](../assets/images/teamstoolkiticon.png)

1. <span data-ttu-id="cb8dc-127">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-127">Select **Create New Project**.</span></span>

    ![Создание проекта](../assets/images/createnewproject.png)

1. <span data-ttu-id="cb8dc-129">Выберите средство quickstart для **Microsoft Teams App и** выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-129">Choose the quickstart tool for **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="cb8dc-130">На странице **Настройка новой страницы проекта** введите имя Project, **расположение** и **имя решения.** </span><span class="sxs-lookup"><span data-stu-id="cb8dc-130">In the **Configure your new project** page, enter the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="cb8dc-131">Выберите решение и проект Place в том же почтовом **ящике каталога.**</span><span class="sxs-lookup"><span data-stu-id="cb8dc-131">Select the **Place solution and project in the same directory** checkbox.</span></span>
1. <span data-ttu-id="cb8dc-132">В **всплывающее** окно Add Capabilities выберите одну или несколько возможностей для установки проекта.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-132">In the **Add Capabilities** pop-up window, choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="cb8dc-133">Выберите **кнопку Далее** для завершения процесса настройки.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-133">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="cb8dc-134">В **всплывающее** окно Add Capabilities выберите свойства для каждой выбранной возможности.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-134">In the **Add Capabilities** pop-up window, choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="cb8dc-135">Нажмите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-135">Select **Finish**.</span></span> <span data-ttu-id="cb8dc-136">Показана **Microsoft Teams набор средств** страница.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-136">The **Microsoft Teams Toolkit** landing page is shown.</span></span>

    ![Teams-страница для наборов инструментов](../assets/images/Teamstoolkitpage.png)

## <a name="configure-your-app"></a><span data-ttu-id="cb8dc-138">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="cb8dc-138">Configure your app</span></span>

<span data-ttu-id="cb8dc-139">В основе приложения Teams три компонента:</span><span class="sxs-lookup"><span data-stu-id="cb8dc-139">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="cb8dc-140">Клиент Microsoft Teams веб,настольный компьютер или мобильный, где пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-140">The Microsoft Teams client including web, desktop, or mobile, where users interact with your app.</span></span>
  1. <span data-ttu-id="cb8dc-141">Сервер, который отвечает на запросы контента, отображаемого в Teams, например, контента вкладок HTML или адаптивной карты бота.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-141">A server that responds to requests for content that is displayed in Teams, for example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="cb8dc-142">Пакет Teams состоит из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="cb8dc-142">A Teams app package consists of three files:</span></span>

      - <span data-ttu-id="cb8dc-143">В manifest.js</span><span class="sxs-lookup"><span data-stu-id="cb8dc-143">The manifest.json</span></span>
      - <span data-ttu-id="cb8dc-144">Значок [цвета](../resources/schema/manifest-schema.md#icons) для отображения приложения в каталоге общедоступных или организаций.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-144">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      - <span data-ttu-id="cb8dc-145">Значок [плана](../resources/schema/manifest-schema.md#icons) для отображения на панели Teams действий.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-145">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="cb8dc-146">При установке приложения клиент Teams определяет файл манифеста, чтобы определить необходимые сведения, такие как имя приложения и URL-адрес, в котором находятся службы.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-146">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="cb8dc-147">Если вы еще этого не сделали, необходимо войти в Microsoft 365 учетную запись, чтобы продолжить процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-147">If you have not done so already, you must sign in to your Microsoft 365 account to continue with the development process.</span></span>
>
> <span data-ttu-id="cb8dc-148">Если у вас нет Microsoft 365 учетной записи, вы можете подписаться на подписку [Microsoft 365 разработчика.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="cb8dc-148">If you do not have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="cb8dc-149">Он бесплатный в течение 90 дней и обновляется до тех пор, пока вы используете его для разработки.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-149">It's free for 90 days and renews as long as you are using it for development activity.</span></span> <span data-ttu-id="cb8dc-150">Если у вас есть подписка Visual Studio Enterprise или Professional, обе программы включают бесплатную подписку Microsoft 365 [разработчика,](https://aka.ms/MyVisualStudioBenefits)активную для Visual Studio подписки.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-150">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="cb8dc-151">Дополнительные сведения см. [в Microsoft 365 подписки разработчика.](/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="cb8dc-151">For more information, see [set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="cb8dc-152">Этапы конфигурации</span><span class="sxs-lookup"><span data-stu-id="cb8dc-152">Configuration steps</span></span>

1. <span data-ttu-id="cb8dc-153">Чтобы настроить приложение на Microsoft Teams набор средств **странице,** выберите **пакет изменить приложение.**</span><span class="sxs-lookup"><span data-stu-id="cb8dc-153">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package**.</span></span>
1. <span data-ttu-id="cb8dc-154">Из **выпадаемого** меню My Environments выберите **разработку.**</span><span class="sxs-lookup"><span data-stu-id="cb8dc-154">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="cb8dc-155">На странице **Сведения о приложении** отредактируете поля свойств вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-155">In the **App details** page, edit your app's property fields.</span></span>
    
    <span data-ttu-id="cb8dc-156">Редактирование полей на странице сведения Приложения обновляет содержимое manifest.jsфайла, который будет отгрузка в составе пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-156">Editing the fields in the App details page updates the contents of the manifest.json file that will ship as part of the app package.</span></span> <span data-ttu-id="cb8dc-157">Дополнительные сведения см. [в Teams набор средств манифесте](https://aka.ms/teams-toolkit-manifest).</span><span class="sxs-lookup"><span data-stu-id="cb8dc-157">For more information, see [Teams Toolkit manifest](https://aka.ms/teams-toolkit-manifest).</span></span>

## <a name="package-your-app"></a><span data-ttu-id="cb8dc-158">Пакет приложения</span><span class="sxs-lookup"><span data-stu-id="cb8dc-158">Package your app</span></span>

<span data-ttu-id="cb8dc-159">Изменение страницы **сведений** о приложении или обновление манифеста **или** **.env-файлов** в папке **.publish** вашего приложения автоматически создаетDevelopment.zip **файл.**</span><span class="sxs-lookup"><span data-stu-id="cb8dc-159">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="cb8dc-160">Файл Development.zip содержит три необходимых файла, **manifest.jsи** два [значка.](../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="cb8dc-160">The Development.zip file includes three required files, the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="cb8dc-161">Установка и локальное запуск приложения</span><span class="sxs-lookup"><span data-stu-id="cb8dc-161">Install and run your app locally</span></span>

1. <span data-ttu-id="cb8dc-162">Из меню **выпадаемой** конфигурации решений выберите **Развертывание,** как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="cb8dc-162">From the **Solution Configurations** dropdown menu, select **Deploy** as shown in the following image:</span></span>

    ![Меню конфигураций решений](../assets/images/solution-configurations.png)

1. <span data-ttu-id="cb8dc-164">Выберите **кнопку IIS Express + Teams.**</span><span class="sxs-lookup"><span data-stu-id="cb8dc-164">Select the **IIS Express + Teams** button.</span></span>

    <span data-ttu-id="cb8dc-165">Диалоговое окно установки приложения отображается в Teams клиенте.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-165">The app installation dialog box appears in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="cb8dc-166">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="cb8dc-166">Validate your app</span></span>

<span data-ttu-id="cb8dc-167">Страница **Проверка** позволяет проверить пакет приложений перед отправкой приложения в AppSource.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-167">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="cb8dc-168">Просто загрузите пакет манифеста, а средство проверки проверит ваше приложение на всех связанных с манифестом тестовых случаях.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-168">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="cb8dc-169">Для каждого неудачного тестирования описание предоставляет ссылку на документацию, которая поможет устранить ошибку.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-169">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="cb8dc-170">Для тестов, которые трудно автоматизировать, в предварительном контрольном списке 7 наиболее распространенных неудачных тестовых случаев, а также ссылки на полный контрольный список отправки. </span><span class="sxs-lookup"><span data-stu-id="cb8dc-170">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="cb8dc-171">Опубликуйте свое приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="cb8dc-171">Publish your app to Teams</span></span>

* <span data-ttu-id="cb8dc-172">На домашней странице проекта можно передать приложение в команду, отправить приложение в настраиваемый магазин приложений вашей компании, чтобы приложением смогли воспользоваться пользователи вашей организации, или отправить приложение в AppSource для всех пользователей Teams.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-172">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

* <span data-ttu-id="cb8dc-173">ИТ-администратор проверит эти отправленные приложения.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-173">Your IT admin will review these submissions.</span></span>

* <span data-ttu-id="cb8dc-174">Вы можете вернуться на страницу **Публикация,** чтобы проверить состояние отправки и узнать, было ли ваше приложение утверждено или отклонено вашим ИТ-администратором. Здесь также можно отправлять обновления в приложение или отменять активные в настоящее время отправки.</span><span class="sxs-lookup"><span data-stu-id="cb8dc-174">You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you can submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="cb8dc-175">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="cb8dc-175">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb8dc-176">Ведение и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="cb8dc-176">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
