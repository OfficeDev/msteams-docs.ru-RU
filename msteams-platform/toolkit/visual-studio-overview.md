---
title: Создание приложений с помощью microsoft Teams набор средств и Visual Studio
description: Начало создания отличных пользовательских приложений непосредственно в Visual Studio с помощью Microsoft Teams набор средств
keywords: набор средств Visual Studio для Teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 08df1d3907a1a3683eb42222e247cd7fd6c0177b
ms.sourcegitcommit: 5e1300d6f4f2ea23beb3cdbbf4bd46999eef4e87
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "49875009"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="6848d-104">Создание приложений с помощью набор средств и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6848d-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="6848d-105">Microsoft Teams набор средств позволяет создавать настраиваемые приложения Teams непосредственно Visual Studio интегрированной среде разработки (IDE).</span><span class="sxs-lookup"><span data-stu-id="6848d-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="6848d-106">Набор средств Microsoft Teams поможет вам в этом процессе и предоставляет все необходимое для создания, отлаки и запуска приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="6848d-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6848d-107">Предварительные условия</span><span class="sxs-lookup"><span data-stu-id="6848d-107">Prerequisites</span></span>

1. [<span data-ttu-id="6848d-108">Включить предварительную версию для разработчиков</span><span class="sxs-lookup"><span data-stu-id="6848d-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="6848d-109">Убедитесь, **<span>что ASP.NE</span>T** и модуль веб-разработки добавлены в Visual Studio экземпляра.</span><span class="sxs-lookup"><span data-stu-id="6848d-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="6848d-110">Чтобы проверить, следуйте шагам в Visual Studio изменения, добавив или удалив [рабочие нагрузки и документацию по компонентам.](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="6848d-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![Модуль asp.net Visual Studio](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="6848d-112">Если вы хотите протестировать приложение, развернув его из Visual Studio, в среде разработки должны быть установлены службы IIS (Internet Information Services).</span><span class="sxs-lookup"><span data-stu-id="6848d-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="6848d-113">Visual Studio не включает IIS и не включается в конфигурацию Windows 10, Windows 8 или Windows 7 по умолчанию; однако вы можете скачать последнюю версию из [Центра загрузки Майкрософт.](https://www.microsoft.com/download/details.aspx?id=48264)</span><span class="sxs-lookup"><span data-stu-id="6848d-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Представление страницы загрузки IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="6848d-115">Установка набор средств</span><span class="sxs-lookup"><span data-stu-id="6848d-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="6848d-116">Приложение Microsoft Teams набор средств для Visual Studio доступно для скачивания из [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)  или непосредственно из меню "Расширения" в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6848d-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="6848d-117">Использование наборов средств</span><span class="sxs-lookup"><span data-stu-id="6848d-117">Using the toolkit</span></span>

- [<span data-ttu-id="6848d-118">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="6848d-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="6848d-119">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="6848d-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="6848d-120">Упаковка приложения</span><span class="sxs-lookup"><span data-stu-id="6848d-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="6848d-121">Запуск приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="6848d-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="6848d-122">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="6848d-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="6848d-123">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="6848d-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="6848d-124">Настройка нового проекта Teams</span><span class="sxs-lookup"><span data-stu-id="6848d-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="6848d-125">Выберите **"Создать новый проект".**</span><span class="sxs-lookup"><span data-stu-id="6848d-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="6848d-126">Выберите **приложение Microsoft Teams и** выберите **"Далее".**</span><span class="sxs-lookup"><span data-stu-id="6848d-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="6848d-127">Появится экран  настройки нового проекта, на котором можно выбрать имя **проекта,** расположение и **имя решения.**</span><span class="sxs-lookup"><span data-stu-id="6848d-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="6848d-128">Пометить поле **"Разместить решение и проект" в одном каталоге.**</span><span class="sxs-lookup"><span data-stu-id="6848d-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="6848d-129">Всплывающее окно с меткой **"Добавить возможности"** позволит выбрать одну или несколько возможностей для настройки проекта.</span><span class="sxs-lookup"><span data-stu-id="6848d-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="6848d-130">Чтобы завершить **процесс** настройки, выберите кнопку "Далее".</span><span class="sxs-lookup"><span data-stu-id="6848d-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="6848d-131">Всплывающее окно с меткой **"Добавить** возможности" позволит выбрать свойства для каждой выбранной возможности.</span><span class="sxs-lookup"><span data-stu-id="6848d-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="6848d-132">Выберите **"Готово",** и вы будете перенастройки на набор средств **Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="6848d-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="6848d-133">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="6848d-133">Configure your app</span></span>

<span data-ttu-id="6848d-134">По сути, приложение Teams включает три компонента:</span><span class="sxs-lookup"><span data-stu-id="6848d-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="6848d-135">Клиент Microsoft Teams (веб-, настольный или мобильный), в котором пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="6848d-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="6848d-136">Сервер, который отвечает на запросы содержимого, которое будет отображаться в Teams, например содержимое вкладки HTML или адаптивная карточка бота.</span><span class="sxs-lookup"><span data-stu-id="6848d-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="6848d-137">Пакет [приложения Teams,](/concepts/build-and-test/apps-package.md) состоящий из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="6848d-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="6848d-138">The manifest.json</span><span class="sxs-lookup"><span data-stu-id="6848d-138">The manifest.json</span></span>
  > - <span data-ttu-id="6848d-139">Значок [цвета](../resources/schema/manifest-schema.md#icons) для вашего приложения, отображаемого в каталоге общедоступных или организаций</span><span class="sxs-lookup"><span data-stu-id="6848d-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="6848d-140">Значок [контура](../resources/schema/manifest-schema.md#icons) для отображения на панели действий Teams.</span><span class="sxs-lookup"><span data-stu-id="6848d-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="6848d-141">При установке приложения клиент Teams проансирует файл манифеста, чтобы определить необходимые сведения, например имя приложения и URL-адрес, где расположены службы.</span><span class="sxs-lookup"><span data-stu-id="6848d-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="6848d-142">Если вы еще не сделали этого, вам потребуется войти в свою учетную запись Microsoft 365 или учетную запись, чтобы продолжить процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="6848d-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="6848d-143">Если у вас нет учетной записи Microsoft 365, вы можете подписаться на программу для разработчиков [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="6848d-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="6848d-144">Он *бесплатный* в течение 90 дней и будет постоянно обновляться, пока вы используете его для разработки.</span><span class="sxs-lookup"><span data-stu-id="6848d-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="6848d-145">Если у вас есть подписка Visual Studio *Корпоративная* или *Профессиональная,* обе программы включают бесплатную подписку разработчика Microsoft 365, активную в течение Visual Studio подписки. [](https://aka.ms/MyVisualStudioBenefits)</span><span class="sxs-lookup"><span data-stu-id="6848d-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="6848d-146">*См.* ["Настройка подписки разработчика Microsoft 365".](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="6848d-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="6848d-147">Этапы конфигурации</span><span class="sxs-lookup"><span data-stu-id="6848d-147">Configuration steps</span></span>

1. <span data-ttu-id="6848d-148">Чтобы настроить приложение, на странице набор средств **Microsoft Teams** выберите "Изменить **пакет приложения".**</span><span class="sxs-lookup"><span data-stu-id="6848d-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="6848d-149">В **выпадаемом меню** "Мои среды" выберите пункт **"Разработка".**</span><span class="sxs-lookup"><span data-stu-id="6848d-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="6848d-150">Вы будете перенаправить поля свойств приложения на странице сведений о приложении. </span><span class="sxs-lookup"><span data-stu-id="6848d-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="6848d-151">При редактировании полей на странице сведений о приложении обновляется содержимое manifest.jsфайла, который в конечном итоге будет погрузка в составе пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="6848d-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="6848d-152">Подробнее</span><span class="sxs-lookup"><span data-stu-id="6848d-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="6848d-153">Упаковка приложения</span><span class="sxs-lookup"><span data-stu-id="6848d-153">Package your app</span></span>

<span data-ttu-id="6848d-154">При **изменении** страницы сведений о приложении или обновлении манифеста или **ENV-файлов** в папке **.publish** приложения автоматически создаетсяDevelopment.zip **файла.**</span><span class="sxs-lookup"><span data-stu-id="6848d-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="6848d-155">Файл Development.zip включает три необходимых файла:manifest.js **и** [два значка.](../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="6848d-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="6848d-156">Установка и запуск приложения локально</span><span class="sxs-lookup"><span data-stu-id="6848d-156">Install and run your app locally</span></span>

1. <span data-ttu-id="6848d-157">В меню **"Конфигурации решений"** выберите пункт **"Развернуть".**</span><span class="sxs-lookup"><span data-stu-id="6848d-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![Меню конфигураций решений](../assets/images/solution-configurations.png)

2. <span data-ttu-id="6848d-159">Выберите **кнопку IIS Express + Teams.**</span><span class="sxs-lookup"><span data-stu-id="6848d-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="6848d-160">Запустится Teams, и диалог установки приложения должен появиться в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="6848d-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="6848d-161">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="6848d-161">Validate your app</span></span>

<span data-ttu-id="6848d-162">Страница **"Проверка"** позволяет проверить пакет приложения перед отправкой приложения в AppSource.</span><span class="sxs-lookup"><span data-stu-id="6848d-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="6848d-163">Просто загрузите пакет манифеста, и средство проверки проверит ваше приложение на всех тестовых случаях, связанных с манифестом.</span><span class="sxs-lookup"><span data-stu-id="6848d-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="6848d-164">Описание каждого неудачного теста содержит ссылку на документацию, которая поможет устранить ошибку.</span><span class="sxs-lookup"><span data-stu-id="6848d-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="6848d-165">Для тестов, которые сложно автоматизировать, в предварительном контрольном списке 7 наиболее распространенных неудачных тестов, а также ссылка на полный контрольный список отправки. </span><span class="sxs-lookup"><span data-stu-id="6848d-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="6848d-166">Публикация приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="6848d-166">Publish your app to Teams</span></span>

<span data-ttu-id="6848d-167">✔ на домашней странице проекта вы можете отправить приложение команде, отправить приложение в пользовательское хранилище приложений компании для пользователей в организации или отправить приложение в источник приложений для всех пользователей Teams.</span><span class="sxs-lookup"><span data-stu-id="6848d-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="6848d-168">✔ эти отправки будут рассмотрены вашим ИТ-администратором.</span><span class="sxs-lookup"><span data-stu-id="6848d-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="6848d-169">✔ вы можете вернуться на  страницу публикации, чтобы проверить состояние отправки и узнать, было ли ваше приложение утверждено или отклонено вашим ИТ-администратором. Кроме того, здесь вы будете отправлять обновления в приложение или отменять все активные в данный момент отправки.</span><span class="sxs-lookup"><span data-stu-id="6848d-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6848d-170">Следующий шаг: обслуживание и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="6848d-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
