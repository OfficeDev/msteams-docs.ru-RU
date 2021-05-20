---
title: Создавайте приложения с помощью Microsoft Teams набор средств и Visual Studio
description: Начать строить большие пользовательские приложения непосредственно в Visual Studio с Microsoft Teams набор средств
keywords: команды визуальный инструментарий студии
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: eb94a8de0355283344ebe890a6fa3a3050e243ea
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566553"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="22c2a-104">Создавайте приложения с помощью Teams набор средств и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="22c2a-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="22c2a-105">Набор средств Microsoft Teams Toolkit позволяет создавать пользовательские приложения Teams непосредственно в интегрированной среде разработки (IDE) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22c2a-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="22c2a-106">Этот набор средств Microsoft Teams предоставит вам пошаговые инструкции в процессе создания приложения, а также все необходимое для сборки, отладки и запуска вашего приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="22c2a-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22c2a-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="22c2a-107">Prerequisites</span></span>

1. <span data-ttu-id="22c2a-108">[Включить предварительный просмотр разработчика](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span><span class="sxs-lookup"><span data-stu-id="22c2a-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

1. <span data-ttu-id="22c2a-109">Убедитесь, что **<span>ASP.NE</span>T и веб-разработки** модуль был добавлен в ваш Visual Studio примере.</span><span class="sxs-lookup"><span data-stu-id="22c2a-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="22c2a-110">Вы можете проверить, следуя шагам в программе [Modify Visual Studio добавлением или удалением рабочих нагрузок и компонентной документации.](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="22c2a-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![визуальный студийный asp.net модуль](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="22c2a-112">Если вы хотите протестировать приложение, разверовав его с Visual Studio, необходимо установить IIS (службы IIS) в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="22c2a-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="22c2a-113">Visual Studio не включает IIS и не входит в список по умолчанию Windows 10, Windows 8 или Windows 7; однако, вы можете скачать последнюю версию из [центра загрузки Майкрософт.](https://www.microsoft.com/download/details.aspx?id=48264)</span><span class="sxs-lookup"><span data-stu-id="22c2a-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Представление страницы загрузки IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="22c2a-115">Установка Teams набор средств</span><span class="sxs-lookup"><span data-stu-id="22c2a-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="22c2a-116">Приложение Microsoft Teams набор средств для Visual Studio доступно для скачивания с [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) или непосредственно из **меню расширений** в течение Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22c2a-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="22c2a-117">Использование инструментария</span><span class="sxs-lookup"><span data-stu-id="22c2a-117">Using the toolkit</span></span>

- [<span data-ttu-id="22c2a-118">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="22c2a-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="22c2a-119">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="22c2a-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="22c2a-120">Пакет приложения</span><span class="sxs-lookup"><span data-stu-id="22c2a-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="22c2a-121">Запустите приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="22c2a-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="22c2a-122">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="22c2a-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="22c2a-123">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="22c2a-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="22c2a-124">Настройка нового проекта Teams технологий</span><span class="sxs-lookup"><span data-stu-id="22c2a-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="22c2a-125">Выберите **Создание нового проекта.**</span><span class="sxs-lookup"><span data-stu-id="22c2a-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="22c2a-126">Выберите **Microsoft Teams и** выберите **Next**.</span><span class="sxs-lookup"><span data-stu-id="22c2a-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="22c2a-127">Вы прибудете на **экране конфигурировать новый** проект, где вы **можете выбрать Project** **имя, местоположение** и **имя решения.**</span><span class="sxs-lookup"><span data-stu-id="22c2a-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="22c2a-128">Проверьте поле помечены **Место решение и проект в том же каталоге**.</span><span class="sxs-lookup"><span data-stu-id="22c2a-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="22c2a-129">Всплывающее окно с пометкой **Add Capabilities** позволит вам выбрать одну или несколько возможностей для настройки проекта.</span><span class="sxs-lookup"><span data-stu-id="22c2a-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="22c2a-130">Выберите **следующую** кнопку для завершения процесса конфигурации.</span><span class="sxs-lookup"><span data-stu-id="22c2a-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="22c2a-131">Всплывающее окно с пометкой **Add Capabilities** позволит вам выбрать свойства для каждой выбранной возможности.</span><span class="sxs-lookup"><span data-stu-id="22c2a-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="22c2a-132">Выберите **финиш,** и вы приземлится **на Microsoft Teams набор средств** странице.</span><span class="sxs-lookup"><span data-stu-id="22c2a-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="22c2a-133">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="22c2a-133">Configure your app</span></span>

<span data-ttu-id="22c2a-134">По своей сути приложение Teams включает в себя три компонента:</span><span class="sxs-lookup"><span data-stu-id="22c2a-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="22c2a-135">Данный Microsoft Teams (веб, настольный или мобильный), где пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="22c2a-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="22c2a-136">Сервер, который отвечает на запросы о содержимом, которое будет отображаться в Teams, например, содержимое вкладки HTML или адаптивная карта бота.</span><span class="sxs-lookup"><span data-stu-id="22c2a-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="22c2a-137">Пакет Teams приложений состоит из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="22c2a-137">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="22c2a-138">manifest.jsна</span><span class="sxs-lookup"><span data-stu-id="22c2a-138">The manifest.json</span></span>
      > - <span data-ttu-id="22c2a-139">Значок [цвета для](../resources/schema/manifest-schema.md#icons) вашего приложения для отображения в общедоступной или организации каталога приложений</span><span class="sxs-lookup"><span data-stu-id="22c2a-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
      > - <span data-ttu-id="22c2a-140">Значок [контура](../resources/schema/manifest-schema.md#icons) для отображения на Teams активности.</span><span class="sxs-lookup"><span data-stu-id="22c2a-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="22c2a-141">Когда приложение установлено, клиент Teams анализирует файл манифеста, чтобы определить необходимую информацию, такую как имя вашего приложения и URL-адрес, где находятся службы.</span><span class="sxs-lookup"><span data-stu-id="22c2a-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="22c2a-142">Если вы еще этого не сделали, вам нужно будет войти в свой аккаунт Microsoft 365 учетную запись, чтобы продолжить процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="22c2a-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="22c2a-143">Если у вас нет учетной Microsoft 365 учетной записи, вы можете подписаться на [подписку Microsoft 365 программы разработчика.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="22c2a-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="22c2a-144">Это бесплатно в *течение* 90 дней и будет постоянно обновляться до тех пор, как вы используете его для развития деятельности.</span><span class="sxs-lookup"><span data-stu-id="22c2a-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="22c2a-145">Если у вас есть Visual Studio *Enterprise* *или Professional* подписка, обе программы включают в себя бесплатную подписку Microsoft 365 [разработчика,](https://aka.ms/MyVisualStudioBenefits)активную в течение всего Visual Studio подписки.</span><span class="sxs-lookup"><span data-stu-id="22c2a-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="22c2a-146">Для получения дополнительной информации [можно настроить Microsoft 365 разработчика.](/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="22c2a-146">For more information, See [Set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="22c2a-147">Этапы конфигурации</span><span class="sxs-lookup"><span data-stu-id="22c2a-147">Configuration steps</span></span>

1. <span data-ttu-id="22c2a-148">Чтобы настроить приложение на странице **Microsoft Teams набор средств,** выберите **пакет приложений Edit.**</span><span class="sxs-lookup"><span data-stu-id="22c2a-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package**.</span></span>
1. <span data-ttu-id="22c2a-149">Из **меню "Мои среды"** выберите **разработку.**</span><span class="sxs-lookup"><span data-stu-id="22c2a-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="22c2a-150">Вы приземлится на странице **деталей** приложения, где вы можете редактировать поля свойств вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="22c2a-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="22c2a-151">Редактирование полей на странице деталей приложения обновляет содержимое файла, manifest.jsв конечном итоге будет поставляться как часть пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="22c2a-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="22c2a-152">Подробнее</span><span class="sxs-lookup"><span data-stu-id="22c2a-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="22c2a-153">Пакет приложения</span><span class="sxs-lookup"><span data-stu-id="22c2a-153">Package your app</span></span>

<span data-ttu-id="22c2a-154">Изменение страницы **деталей приложения** или обновление **манифеста,** **или файлов .env** в папке  **.publish** вашего приложения автоматически **генерирует вашDevelopment.zip** файл.</span><span class="sxs-lookup"><span data-stu-id="22c2a-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="22c2a-155">Файл Development.zip в себя три необходимых файла - **manifest.jsи** [две иконки.](../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="22c2a-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="22c2a-156">Установка и запуск приложения локально</span><span class="sxs-lookup"><span data-stu-id="22c2a-156">Install and run your app locally</span></span>

1. <span data-ttu-id="22c2a-157">Из **меню высадки конфигураций** решений выберите **Развертывание, как** показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="22c2a-157">From the **Solution Configurations** dropdown menu, select **Deploy** as shown in the following image:</span></span>

    ![Меню конфигураций решений](../assets/images/solution-configurations.png)

2. <span data-ttu-id="22c2a-159">Выберите **IIS Express и Teams кнопку.**</span><span class="sxs-lookup"><span data-stu-id="22c2a-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="22c2a-160">Teams запуск и диалог установки приложения должны появиться в Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="22c2a-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="22c2a-161">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="22c2a-161">Validate your app</span></span>

<span data-ttu-id="22c2a-162">Страница **проверки** позволяет проверить пакет приложений перед отправкой приложения на AppSource.</span><span class="sxs-lookup"><span data-stu-id="22c2a-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="22c2a-163">Просто загрузите пакет манифеста и инструмент проверки проверит ваше приложение на всех явных связанных тестовых случаях.</span><span class="sxs-lookup"><span data-stu-id="22c2a-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="22c2a-164">Для каждого неудавшегося теста описание предоставляет ссылку на документацию, которая поможет вам исправить ошибку.</span><span class="sxs-lookup"><span data-stu-id="22c2a-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="22c2a-165">Для тестов, которые трудно автоматизировать, Предварительный контрольный **список** подробно 7 из наиболее распространенных неудачных тестовых случаев, а также ссылку на полный контрольный список представления.</span><span class="sxs-lookup"><span data-stu-id="22c2a-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="22c2a-166">Опубликуйте свое приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="22c2a-166">Publish your app to Teams</span></span>

<span data-ttu-id="22c2a-167">✔ На главной странице проекта вы можете загрузить приложение в группу, отправить приложение в пользовательский магазин приложений компании для пользователей вашей организации или отправить приложение в App Source для всех Teams пользователей.</span><span class="sxs-lookup"><span data-stu-id="22c2a-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="22c2a-168">✔ ИТ-администратор рассмотрит эти материалы.</span><span class="sxs-lookup"><span data-stu-id="22c2a-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="22c2a-169">✔ Вы можете вернуться на страницу **Публикации,** чтобы проверить свой статус отправки и узнать, было ли ваше приложение одобрено или отклонено вашим ИТ-администратором. Здесь же вы будете отправлять обновления в приложение или отменять любые активные в настоящее время материалы.</span><span class="sxs-lookup"><span data-stu-id="22c2a-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="22c2a-170">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="22c2a-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="22c2a-171">Поддержание и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="22c2a-171">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
