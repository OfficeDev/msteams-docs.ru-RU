---
title: Создание приложений с помощью microsoft Teams набор средств и Visual Studio
description: Начало создания больших пользовательских приложений непосредственно в Visual Studio с microsoft Teams набор средств
keywords: набор инструментов для визуальной студии teams
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: bf8250e42bdf96073d729a19e921c400f242c67a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020255"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="f119f-104">Создайте приложения с набор средств и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f119f-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="f119f-105">Набор средств Microsoft Teams Toolkit позволяет создавать пользовательские приложения Teams непосредственно в интегрированной среде разработки (IDE) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f119f-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="f119f-106">Этот набор средств Microsoft Teams предоставит вам пошаговые инструкции в процессе создания приложения, а также все необходимое для сборки, отладки и запуска вашего приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="f119f-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f119f-107">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="f119f-107">Prerequisites</span></span>

1. [<span data-ttu-id="f119f-108">Включить предварительный просмотр разработчика</span><span class="sxs-lookup"><span data-stu-id="f119f-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="f119f-109">Убедитесь, **<span>что ASP.NE</span>T** и модуль веб-разработки добавлены в экземпляр Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f119f-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="f119f-110">Вы можете проверить, следуя шагам в Visual Studio, добавив или удалив рабочие [нагрузки и документацию по компонентам.](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f119f-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![модуль asp.net студии](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="f119f-112">Если вы хотите протестировать приложение, развернув его из Visual Studio, необходимо установить службы IIS (Internet Information Services) в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="f119f-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="f119f-113">Visual Studio не включает IIS и не входит в конфигурацию Windows 10, Windows 8 Или Windows 7; Однако вы можете скачать последнюю версию из [центра загрузки Майкрософт.](https://www.microsoft.com/download/details.aspx?id=48264)</span><span class="sxs-lookup"><span data-stu-id="f119f-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Представление страницы IIS для скачивания](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="f119f-115">Установка команд набор средств</span><span class="sxs-lookup"><span data-stu-id="f119f-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="f119f-116">Приложение Microsoft Teams набор средств для Visual Studio доступно для скачивания с [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)  или непосредственно из меню Расширения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f119f-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="f119f-117">Использование инструментария</span><span class="sxs-lookup"><span data-stu-id="f119f-117">Using the toolkit</span></span>

- [<span data-ttu-id="f119f-118">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="f119f-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="f119f-119">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="f119f-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="f119f-120">Пакет приложения</span><span class="sxs-lookup"><span data-stu-id="f119f-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="f119f-121">Запуск приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="f119f-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="f119f-122">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="f119f-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="f119f-123">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="f119f-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="f119f-124">Настройка нового проекта Teams</span><span class="sxs-lookup"><span data-stu-id="f119f-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="f119f-125">Выберите **Создание нового проекта.**</span><span class="sxs-lookup"><span data-stu-id="f119f-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="f119f-126">Выберите **приложение Microsoft Teams и** выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f119f-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="f119f-127">Вы прибудете на экран **Настройка нового** экрана проекта, на котором можно выбрать имя **Project,** **Расположение** и **имя решения.**</span><span class="sxs-lookup"><span data-stu-id="f119f-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="f119f-128">Проверьте поле с **меткой Place solution and project в том же каталоге.**</span><span class="sxs-lookup"><span data-stu-id="f119f-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="f119f-129">Всплывающее окно с **меткой Add Capabilities** позволит выбрать одну или несколько возможностей для установки проекта.</span><span class="sxs-lookup"><span data-stu-id="f119f-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="f119f-130">Выберите **кнопку Далее** для завершения процесса настройки.</span><span class="sxs-lookup"><span data-stu-id="f119f-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="f119f-131">Всплывающее окно с **меткой Add Capabilities** позволит выбрать свойства для каждой выбранной возможности.</span><span class="sxs-lookup"><span data-stu-id="f119f-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="f119f-132">Выберите **Finish,** и вы приземлиться на странице **Microsoft Teams набор средств.**</span><span class="sxs-lookup"><span data-stu-id="f119f-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="f119f-133">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="f119f-133">Configure your app</span></span>

<span data-ttu-id="f119f-134">В основе приложения Teams три компонента:</span><span class="sxs-lookup"><span data-stu-id="f119f-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="f119f-135">Клиент Microsoft Teams (веб-, настольный или мобильный), в котором пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="f119f-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="f119f-136">Сервер, который отвечает на запросы контента, который будет отображаться в Teams, например, содержимое вкладок HTML или адаптивная карта бота.</span><span class="sxs-lookup"><span data-stu-id="f119f-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="f119f-137">Пакет приложений [Teams,](/concepts/build-and-test/apps-package.md) состоящий из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="f119f-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="f119f-138">В manifest.js</span><span class="sxs-lookup"><span data-stu-id="f119f-138">The manifest.json</span></span>
  > - <span data-ttu-id="f119f-139">Значок [цвета](../resources/schema/manifest-schema.md#icons) для вашего приложения, отображаемого в каталоге общедоступных или организаций приложений</span><span class="sxs-lookup"><span data-stu-id="f119f-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="f119f-140">Значок [плана](../resources/schema/manifest-schema.md#icons) для отображения в панели действий Teams.</span><span class="sxs-lookup"><span data-stu-id="f119f-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="f119f-141">При установке приложения клиент Teams определяет файл манифеста, чтобы определить необходимые сведения, такие как имя приложения и URL-адрес, в котором находятся службы.</span><span class="sxs-lookup"><span data-stu-id="f119f-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="f119f-142">Если вы еще этого не сделали, вам потребуется войти в microsoft 365 или учетную запись, чтобы продолжить процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="f119f-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="f119f-143">Если у вас нет учетной записи Microsoft 365, вы можете подписаться на подписку на программу разработчиков [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="f119f-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="f119f-144">Он *бесплатный в* течение 90 дней и будет постоянно обновляться до тех пор, пока вы используете его для разработки.</span><span class="sxs-lookup"><span data-stu-id="f119f-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="f119f-145">Если у вас есть подписка Visual Studio *enterprise* или *Professional,* обе программы включают бесплатную подписку на разработчика Microsoft 365, активную для Visual Studio подписки. [](https://aka.ms/MyVisualStudioBenefits)</span><span class="sxs-lookup"><span data-stu-id="f119f-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="f119f-146">*Настройка* [подписки на разработчика Microsoft 365.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="f119f-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="f119f-147">Этапы конфигурации</span><span class="sxs-lookup"><span data-stu-id="f119f-147">Configuration steps</span></span>

1. <span data-ttu-id="f119f-148">Чтобы настроить приложение, на странице **Microsoft Teams набор средств** выберите пакет изменить **приложение.**</span><span class="sxs-lookup"><span data-stu-id="f119f-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="f119f-149">Из **выпадаемого** меню My Environments выберите **разработку.**</span><span class="sxs-lookup"><span data-stu-id="f119f-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="f119f-150">Вы приземлите страницу **сведений о приложении,** на которой можно изменить поля свойств вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f119f-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="f119f-151">Редактирование полей на странице сведения приложения обновляет содержимое manifest.jsфайла, который в конечном итоге будет отгрузка в составе пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="f119f-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="f119f-152">Подробнее</span><span class="sxs-lookup"><span data-stu-id="f119f-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="f119f-153">Пакет приложения</span><span class="sxs-lookup"><span data-stu-id="f119f-153">Package your app</span></span>

<span data-ttu-id="f119f-154">Изменение страницы **сведений** о приложении или обновление манифеста **или** **.env-файлов** в папке **.publish** вашего приложения автоматически создаетDevelopment.zip **файл.**</span><span class="sxs-lookup"><span data-stu-id="f119f-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="f119f-155">Файл Development.zip содержит три необходимых файла : **manifest.jsи** [два значка.](../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="f119f-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="f119f-156">Установка и локальное запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f119f-156">Install and run your app locally</span></span>

1. <span data-ttu-id="f119f-157">Из меню **выпадаемой** конфигурации решений выберите **Развертывание.**</span><span class="sxs-lookup"><span data-stu-id="f119f-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![Меню конфигураций решений](../assets/images/solution-configurations.png)

2. <span data-ttu-id="f119f-159">Выберите **кнопку IIS Express + Teams.**</span><span class="sxs-lookup"><span data-stu-id="f119f-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="f119f-160">Команды будут запущены, и диалог установки приложения должен отображаться в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="f119f-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="f119f-161">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="f119f-161">Validate your app</span></span>

<span data-ttu-id="f119f-162">Страница **Проверка** позволяет проверить пакет приложений перед отправкой приложения в AppSource.</span><span class="sxs-lookup"><span data-stu-id="f119f-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="f119f-163">Просто загрузите пакет манифеста, а средство проверки проверит ваше приложение на всех связанных с манифестом тестовых случаях.</span><span class="sxs-lookup"><span data-stu-id="f119f-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="f119f-164">Для каждого неудачного тестирования описание предоставляет ссылку на документацию, которая поможет устранить ошибку.</span><span class="sxs-lookup"><span data-stu-id="f119f-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="f119f-165">Для тестов, которые трудно автоматизировать, в предварительном контрольном списке 7 наиболее распространенных неудачных тестовых случаев, а также ссылки на полный контрольный список отправки. </span><span class="sxs-lookup"><span data-stu-id="f119f-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="f119f-166">Опубликуйте свое приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="f119f-166">Publish your app to Teams</span></span>

<span data-ttu-id="f119f-167">✔ На домашней странице проекта вы можете загрузить приложение в команду, отправить приложение в пользовательский магазин приложений для пользователей организации или отправить приложение в App Source для всех пользователей Teams.</span><span class="sxs-lookup"><span data-stu-id="f119f-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="f119f-168">✔ ИТ-администратор рассмотрит эти материалы.</span><span class="sxs-lookup"><span data-stu-id="f119f-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="f119f-169">✔ Вы можете вернуться на страницу **Публикация,** чтобы проверить состояние отправки и узнать, было ли ваше приложение утверждено или отклонено вашим ИТ-администратором. Кроме того, здесь вы придете для отправки обновлений в ваше приложение или отмены любых активных представлений.</span><span class="sxs-lookup"><span data-stu-id="f119f-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f119f-170">Следующий шаг: сохранение и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="f119f-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
