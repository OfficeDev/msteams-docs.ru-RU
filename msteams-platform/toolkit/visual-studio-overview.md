---
title: Создание приложений с помощью набора инструментов Microsoft Teams и Visual Studio
description: Приступая к созданию привлекательных пользовательских приложений непосредственно в Visual Studio с помощью набора инструментов Microsoft Teams
keywords: набор средств Visual Studio для Teams
ms.topic: overview
ms.openlocfilehash: 33005174dc1e12e6473522e7d7ee09920a989689
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652118"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a><span data-ttu-id="d044b-104">Создание приложений с помощью набора инструментов Microsoft Teams и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d044b-104">Build apps with the Microsoft Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="d044b-105">Набор средств Microsoft Teams позволяет создавать пользовательские приложения Teams непосредственно в интегрированной среде разработки Visual Studio (IDE).</span><span class="sxs-lookup"><span data-stu-id="d044b-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="d044b-106">Набор средств Microsoft Teams поможет вам выполнить все необходимые действия для создания, отладки и запуска приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="d044b-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d044b-107">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="d044b-107">Prerequisites</span></span>

1. [<span data-ttu-id="d044b-108">Включение предварительной версии для разработчиков</span><span class="sxs-lookup"><span data-stu-id="d044b-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="d044b-109">Убедитесь, что в экземпляр Visual Studio добавлен **модуль <span>ASP.NE</span>T и веб-разработки** .</span><span class="sxs-lookup"><span data-stu-id="d044b-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="d044b-110">Вы можете проверить их, выполнив действия, описанные в разделе [изменение Visual Studio, добавив или удалив рабочие нагрузки и](/visualstudio/install/modify-visual-studio?view=vs-2019) документацию по компонентам.</span><span class="sxs-lookup"><span data-stu-id="d044b-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019) documentation.</span></span>

![модуль Visual Studio asp.net](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="d044b-112">Если вы хотите протестировать приложение, развертывая его из Visual Studio, вам потребуется установить службы IIS (Internet Information Services) в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="d044b-112">If you would like test your app by deploy it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="d044b-113">Visual Studio не включает IIS и не включается в конфигурацию Windows 10, Windows 8 или Windows 7 по умолчанию; Однако последнюю версию можно скачать в [центре загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=48264.)</span><span class="sxs-lookup"><span data-stu-id="d044b-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264.)</span></span>

![Представление страницы скачивания IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="d044b-115">Установка набора инструментов Teams</span><span class="sxs-lookup"><span data-stu-id="d044b-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="d044b-116">Набор средств Microsoft Teams для Visual Studio доступен для загрузки из [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) или непосредственно из меню **расширения** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d044b-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="d044b-117">Использование набора средств</span><span class="sxs-lookup"><span data-stu-id="d044b-117">Using the toolkit</span></span>

- [<span data-ttu-id="d044b-118">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="d044b-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="d044b-119">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="d044b-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="d044b-120">Упаковка приложения</span><span class="sxs-lookup"><span data-stu-id="d044b-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="d044b-121">Запуск приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="d044b-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="d044b-122">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="d044b-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="d044b-123">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="d044b-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="d044b-124">Настройка нового проекта Teams</span><span class="sxs-lookup"><span data-stu-id="d044b-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="d044b-125">Выберите **создать новый проект**.</span><span class="sxs-lookup"><span data-stu-id="d044b-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="d044b-126">Выберите **приложение Microsoft Teams** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d044b-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="d044b-127">Вы будете приступать к экрану **Настройка нового проекта** , где можно выбрать **имя проекта**, **Расположение**и **имя решения**.</span><span class="sxs-lookup"><span data-stu-id="d044b-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="d044b-128">Установите флажок пометить **решение и проект в одном и том же каталоге**.</span><span class="sxs-lookup"><span data-stu-id="d044b-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="d044b-129">Всплывающее окно с подписью **добавить возможности** позволит выбрать одну или несколько возможностей для настройки проекта.</span><span class="sxs-lookup"><span data-stu-id="d044b-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="d044b-130">Нажмите кнопку **Далее** , чтобы завершить процесс настройки.</span><span class="sxs-lookup"><span data-stu-id="d044b-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="d044b-131">Всплывающее окно с пометкой **добавить возможности** позволит выбрать свойства для каждой выбранной возможности.</span><span class="sxs-lookup"><span data-stu-id="d044b-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="d044b-132">Нажмите кнопку **Готово** , и вы будете намерены на начальной странице **набора инструментов Microsoft Teams** .</span><span class="sxs-lookup"><span data-stu-id="d044b-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="d044b-133">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="d044b-133">Configure your app</span></span>

<span data-ttu-id="d044b-134">В основном приложение Teams поработает с тремя компонентами:</span><span class="sxs-lookup"><span data-stu-id="d044b-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="d044b-135">Клиент Microsoft Teams (веб-сайт, Настольный компьютер или мобильное устройство), на котором пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="d044b-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="d044b-136">Сервер, который отвечает на запросы для контента, который будет отображаться в Teams, например, контент вкладки HTML или адаптивной карточки Bot.</span><span class="sxs-lookup"><span data-stu-id="d044b-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="d044b-137">[Пакет приложения](/concepts/build-and-test/apps-package.md) Teams состоит из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="d044b-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="d044b-138">manifest.jsна</span><span class="sxs-lookup"><span data-stu-id="d044b-138">The manifest.json</span></span>
  > - <span data-ttu-id="d044b-139">[Значок цвета](../resources/schema/manifest-schema.md#icons) приложения для отображения в каталоге приложений "общедоступный" или "Организация"</span><span class="sxs-lookup"><span data-stu-id="d044b-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="d044b-140">[Значок структуры](../resources/schema/manifest-schema.md#icons) для отображения на панели активности Teams.</span><span class="sxs-lookup"><span data-stu-id="d044b-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="d044b-141">При установке приложения клиент Teams анализирует файл манифеста, чтобы определить необходимые сведения, такие как имя вашего приложения и URL-адрес, по которому расположены службы.</span><span class="sxs-lookup"><span data-stu-id="d044b-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="d044b-142">Если вы еще не сделали этого, вам потребуется войти в систему Microsoft 365 или учетную запись, чтобы продолжить процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="d044b-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="d044b-143">Если у вас нет учетной записи Microsoft 365, вы можете подписаться на подписку на [программу для разработчиков microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program) .</span><span class="sxs-lookup"><span data-stu-id="d044b-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="d044b-144">Он *освободится* на 90 дней и будет обновляться до тех пор, пока вы его используете для разработки действий.</span><span class="sxs-lookup"><span data-stu-id="d044b-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="d044b-145">Если у вас есть подписка на Visual Studio *Enterprise* или *Professional* , обе программы включают бесплатную [подписку](https://aka.ms/MyVisualStudioBenefits)на Microsoft 365 для разработчиков, действующую в течение всего срока действия вашей подписки на Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d044b-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="d044b-146">*Ознакомьтесь* [со статьей Настройка подписки на Microsoft 365 для разработчиков](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span><span class="sxs-lookup"><span data-stu-id="d044b-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="d044b-147">Этапы конфигурации</span><span class="sxs-lookup"><span data-stu-id="d044b-147">Configuration steps</span></span>

1. <span data-ttu-id="d044b-148">Чтобы настроить приложение, на начальной странице **набора инструментов Microsoft Teams** выберите **изменить пакет приложения** .</span><span class="sxs-lookup"><span data-stu-id="d044b-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="d044b-149">В раскрывающемся меню **Мои среды** выберите пункт **Разработка**.</span><span class="sxs-lookup"><span data-stu-id="d044b-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="d044b-150">На странице **сведения о приложении** вы можете изменить поля свойств приложения.</span><span class="sxs-lookup"><span data-stu-id="d044b-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="d044b-151">Изменение полей на странице "сведения о приложении" обновляет содержимое manifest.jsв файле, который в конечном итоге будет поставляться в составе пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="d044b-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="d044b-152">Подробнее</span><span class="sxs-lookup"><span data-stu-id="d044b-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="d044b-153">Упаковка приложения</span><span class="sxs-lookup"><span data-stu-id="d044b-153">Package your app</span></span>

<span data-ttu-id="d044b-154">Изменение страницы **сведений о приложении** или обновление **манифеста**или файлов **env** в папке **публикации** приложения автоматически создаст файл **Development.zip** .</span><span class="sxs-lookup"><span data-stu-id="d044b-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="d044b-155">Файл Development.zip состоит из трех обязательных файлов: **manifest.jsдля** и [двух файлов значков](../concepts/build-and-test/apps-package.md#icons).</span><span class="sxs-lookup"><span data-stu-id="d044b-155">The Development.zip file includes three required files — the **manifest.json** and [two icon files](../concepts/build-and-test/apps-package.md#icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="d044b-156">Установка и запуск приложения на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="d044b-156">Install and run your app locally</span></span>

1. <span data-ttu-id="d044b-157">В раскрывающемся меню **конфигурации решения** выберите команду **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="d044b-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![Меню конфигураций решения](../assets/images/solution-configurations.png)

2. <span data-ttu-id="d044b-159">Нажмите кнопку **ISS Express + Teams** .</span><span class="sxs-lookup"><span data-stu-id="d044b-159">Select the **ISS Express + Teams** button.</span></span>

1. <span data-ttu-id="d044b-160">Запускаются Teams, а диалоговое окно установки приложения должно отображаться в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="d044b-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="d044b-161">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="d044b-161">Validate your app</span></span>

<span data-ttu-id="d044b-162">Страница **проверки** позволяет проверить пакет приложения перед отправкой приложения в AppSource.</span><span class="sxs-lookup"><span data-stu-id="d044b-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="d044b-163">Просто отправьте пакет манифеста, и средство проверки проверит ваше приложение на соответствие всем тестовым случаям, связанным с манифестом.</span><span class="sxs-lookup"><span data-stu-id="d044b-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="d044b-164">Для каждого неудачных тестов в описании представлена ссылка на документацию, которая поможет исправить ошибку.</span><span class="sxs-lookup"><span data-stu-id="d044b-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="d044b-165">Для тестов, которые трудно автоматизировать, **Предварительный контрольный список** включает 7 наиболее распространенных тестовых случаев, а также ссылки на полный контрольный список отправки.</span><span class="sxs-lookup"><span data-stu-id="d044b-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="d044b-166">Публикация приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="d044b-166">Publish your app to Teams</span></span>

<span data-ttu-id="d044b-167">✔ На домашней странице проекта вы можете отправить свое приложение в группу, отправить свое приложение в пользовательскую магазин приложений для пользователей в вашей организации или отправить свое приложение в источник приложений для всех пользователей Teams.</span><span class="sxs-lookup"><span data-stu-id="d044b-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="d044b-168">✔ ИТ ИТ ИТ, просматривая эти отправки.</span><span class="sxs-lookup"><span data-stu-id="d044b-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="d044b-169">✔ Вы можете вернуться на страницу **публикации** , чтобы проверить состояние отправки и узнать, было ли ваше приложение утверждено или отклонено вашим ИТ-администратором. Кроме того, здесь вы будете передавать обновления в свое приложение или отменять все активные в данный момент отправки.</span><span class="sxs-lookup"><span data-stu-id="d044b-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d044b-170">Следующий шаг: обслуживание и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="d044b-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>