---
title: Создание приложений с помощью набора средств Microsoft Teams и Visual Studio
description: Приступите к созданию отличного создания пользовательских приложений непосредственно в Visual Studio с помощью набора средств Microsoft Teams Toolkit
keywords: набор средств visual Studio для teams
ms.topic: overview
ms.openlocfilehash: 79ea22cfd154313247132c22684d444c0813c66f
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819205"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a><span data-ttu-id="47cfd-104">Создание приложений с помощью набора средств Microsoft Teams и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="47cfd-104">Build apps with the Microsoft Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="47cfd-105">Набор средств Microsoft Teams позволяет создавать настраиваемые приложения Teams прямо в интегрированной среде разработки Visual Studio (IDE).</span><span class="sxs-lookup"><span data-stu-id="47cfd-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="47cfd-106">Набор средств Microsoft Teams поможет вам выполнить все необходимые действия для сборки, отладки и запуска приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="47cfd-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47cfd-107">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="47cfd-107">Prerequisites</span></span>

1. [<span data-ttu-id="47cfd-108">Включение предварительной версии для разработчиков</span><span class="sxs-lookup"><span data-stu-id="47cfd-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="47cfd-109">Убедитесь, что \*\* <span>ASP.NE</span>T и модуль веб-разработки\*\* были добавлены в экземпляр Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="47cfd-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="47cfd-110">Чтобы проверить эти действия, выполните действия [в изменении Visual Studio, добавив или удалив документацию по компонентам.](/visualstudio/install/modify-visual-studio?view=vs-2019)</span><span class="sxs-lookup"><span data-stu-id="47cfd-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019) documentation.</span></span>

![модуль asp.net Visual Studio](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="47cfd-112">Если вы хотите протестировать приложение путем развертывания из Visual Studio, в среде разработки должны быть установлены службы IIS (Internet Information Services).</span><span class="sxs-lookup"><span data-stu-id="47cfd-112">If you would like test your app by deploy it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="47cfd-113">Visual Studio не включает службы IIS и не включается в конфигурацию Windows 10 по умолчанию, Windows 8 или Windows 7; Тем не менее, можно скачать последнюю версию в Центре [загрузки Майкрософт.](https://www.microsoft.com/download/details.aspx?id=48264)</span><span class="sxs-lookup"><span data-stu-id="47cfd-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Представление страницы загрузки IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="47cfd-115">Установка набора средств Teams</span><span class="sxs-lookup"><span data-stu-id="47cfd-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="47cfd-116">Набор средств Microsoft Teams для Visual Studio доступен для загрузки из [набора visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) или непосредственно из **меню расширений** visual Studio.</span><span class="sxs-lookup"><span data-stu-id="47cfd-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="47cfd-117">Использование набора средств</span><span class="sxs-lookup"><span data-stu-id="47cfd-117">Using the toolkit</span></span>

- [<span data-ttu-id="47cfd-118">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="47cfd-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="47cfd-119">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="47cfd-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="47cfd-120">Упаковка приложения</span><span class="sxs-lookup"><span data-stu-id="47cfd-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="47cfd-121">Запуск приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="47cfd-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="47cfd-122">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="47cfd-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="47cfd-123">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="47cfd-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="47cfd-124">Настройка нового проекта Teams</span><span class="sxs-lookup"><span data-stu-id="47cfd-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="47cfd-125">Выберите **"Создать проект".**</span><span class="sxs-lookup"><span data-stu-id="47cfd-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="47cfd-126">Choose **Microsoft Teams App** and select **Next.**</span><span class="sxs-lookup"><span data-stu-id="47cfd-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="47cfd-127">Перейдите на экран "Настройка нового **проекта",** в котором вы можете выбрать **имя проекта,** **расположение**и **имя решения.**</span><span class="sxs-lookup"><span data-stu-id="47cfd-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="47cfd-128">Установите флажок **"Размещение" и проект в том же каталоге.**</span><span class="sxs-lookup"><span data-stu-id="47cfd-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="47cfd-129">Во всплывающем окне с **меткой "Дополнительные возможности"** можно выбрать одну или несколько возможностей для настройки проекта.</span><span class="sxs-lookup"><span data-stu-id="47cfd-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="47cfd-130">Нажмите **кнопку** "Далее", чтобы завершить настройку.</span><span class="sxs-lookup"><span data-stu-id="47cfd-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="47cfd-131">Во всплывающем окне с **меткой "Дополнительные возможности"** можно выбрать свойства для каждой из выбранных возможностей.</span><span class="sxs-lookup"><span data-stu-id="47cfd-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="47cfd-132">Нажмите **кнопку** "Готово", на какой-то время вы перешли на **любую** страницу Набора средств Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="47cfd-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="47cfd-133">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="47cfd-133">Configure your app</span></span>

<span data-ttu-id="47cfd-134">В своей ядре приложение Teams использует три компонента:</span><span class="sxs-lookup"><span data-stu-id="47cfd-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="47cfd-135">Клиент Microsoft Teams (веб-клиент, классический или мобильный), с помощью которого пользователи взаимодействуют с приложением.</span><span class="sxs-lookup"><span data-stu-id="47cfd-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="47cfd-136">Сервер, отвечающий на запросы контента, которое будет отображаться в Teams, например содержимое HTML-вкладки или адаптивная карточка бота.</span><span class="sxs-lookup"><span data-stu-id="47cfd-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="47cfd-137">Пакет приложения [Teams, состоящий](/concepts/build-and-test/apps-package.md) из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="47cfd-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="47cfd-138">manifest.js</span><span class="sxs-lookup"><span data-stu-id="47cfd-138">The manifest.json</span></span>
  > - <span data-ttu-id="47cfd-139">[Цветовой значок](../resources/schema/manifest-schema.md#icons) для вашего приложения станут отображаться в общедоступном каталоге или каталоге приложений организации.</span><span class="sxs-lookup"><span data-stu-id="47cfd-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="47cfd-140">Значок [структуры, который](../resources/schema/manifest-schema.md#icons) отображается на панели действий Teams.</span><span class="sxs-lookup"><span data-stu-id="47cfd-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="47cfd-141">При установке приложения клиент Teams анализирует файл манифеста и определяет нужные данные, такие как имя приложения и URL-адрес служб.</span><span class="sxs-lookup"><span data-stu-id="47cfd-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="47cfd-142">Если вы еще не выполнили этого, вам потребуется войти в свою учетную запись Microsoft 365 или учетную запись, чтобы продолжить процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="47cfd-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="47cfd-143">Если у вас нет учетной записи Microsoft 365, вы можете получить ее, чтобы получить [ее, воспоминая программа для разработчиков Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="47cfd-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="47cfd-144">Она *бесплатна* в течение 90 дней и будет постоянно продлеваться при ее использовании для разработки.</span><span class="sxs-lookup"><span data-stu-id="47cfd-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="47cfd-145">Если у вас подписка на Visual Studio *Корпоративная* или профессиональная, в обе программы входят бесплатная подписка разработчика Microsoft 365, действуяна на срок действия подписки на Visual Studio. *Professional* [developer subscription](https://aka.ms/MyVisualStudioBenefits)</span><span class="sxs-lookup"><span data-stu-id="47cfd-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="47cfd-146">*См.* [статью "Настройка подписки разработчика Microsoft 365".](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="47cfd-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="47cfd-147">Этапы конфигурации</span><span class="sxs-lookup"><span data-stu-id="47cfd-147">Configuration steps</span></span>

1. <span data-ttu-id="47cfd-148">Чтобы настроить приложение, на падущей **странице набора средств Microsoft Teams выберите** **"Изменить пакет приложения".**</span><span class="sxs-lookup"><span data-stu-id="47cfd-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="47cfd-149">В раскрывающемся **меню "Мои** среды" выберите **"Разработка".**</span><span class="sxs-lookup"><span data-stu-id="47cfd-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="47cfd-150">Вы перешли на **страницу сведений** о приложении, на которой вы можете изменить поля свойств приложения.</span><span class="sxs-lookup"><span data-stu-id="47cfd-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="47cfd-151">При изменении полей на странице сведений о приложении обновляется содержимое manifest.js-файла, который в итоге появляется в составе пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="47cfd-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="47cfd-152">Подробнее</span><span class="sxs-lookup"><span data-stu-id="47cfd-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="47cfd-153">Упаковка приложения</span><span class="sxs-lookup"><span data-stu-id="47cfd-153">Package your app</span></span>

<span data-ttu-id="47cfd-154">При изменении **страницы сведений** о приложении **или**изменении манифеста, **или файлы .env** в папке  **.publish** приложения \*\* автоматически создаютсяDevelopment.zip\*\* файл.</span><span class="sxs-lookup"><span data-stu-id="47cfd-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="47cfd-155">В Development.zip включается три необходимых файла **—manifest.jsи** два файла [значка.](../concepts/build-and-test/apps-package.md#icons)</span><span class="sxs-lookup"><span data-stu-id="47cfd-155">The Development.zip file includes three required files — the **manifest.json** and [two icon files](../concepts/build-and-test/apps-package.md#icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="47cfd-156">Установка и запуск приложения на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="47cfd-156">Install and run your app locally</span></span>

1. <span data-ttu-id="47cfd-157">В раскрывающемся **меню "Конфигурации решений"** выберите **"Развернуть".**</span><span class="sxs-lookup"><span data-stu-id="47cfd-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![Меню "Конфигурации решения"](../assets/images/solution-configurations.png)

2. <span data-ttu-id="47cfd-159">Нажмите **кнопку ISS Express + Teams.**</span><span class="sxs-lookup"><span data-stu-id="47cfd-159">Select the **ISS Express + Teams** button.</span></span>

1. <span data-ttu-id="47cfd-160">Запустится Teams, а в клиенте Teams появится диалоговое окно установки приложения.</span><span class="sxs-lookup"><span data-stu-id="47cfd-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="47cfd-161">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="47cfd-161">Validate your app</span></span>

<span data-ttu-id="47cfd-162">На **странице "Проверка"** можно проверить пакет приложения перед отправкой приложения в AppSource.</span><span class="sxs-lookup"><span data-stu-id="47cfd-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="47cfd-163">Просто отправьте пакет манифеста и средство проверки сверит ваше приложение по всем требованиям тестовых случаев.</span><span class="sxs-lookup"><span data-stu-id="47cfd-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="47cfd-164">Для каждой неудачной проверки описание содержит ссылку на документацию, помогающую устранить ошибку.</span><span class="sxs-lookup"><span data-stu-id="47cfd-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="47cfd-165">Для тестов, сложных для автоматизации, контрольный **список** подробно статуса 7 наиболее распространенных неудачных тестовых случаев, а также ссылки на полный контрольный список отправки.</span><span class="sxs-lookup"><span data-stu-id="47cfd-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="47cfd-166">Публикация приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="47cfd-166">Publish your app to Teams</span></span>

<span data-ttu-id="47cfd-167">✔ на домашней странице проекта вы можете отправить его в команду, отправить приложение в пользовательское хранилище приложений вашей компании для пользователей в вашей организации или отправить свое приложение в исходный код приложений для всех пользователей Teams.</span><span class="sxs-lookup"><span data-stu-id="47cfd-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="47cfd-168">✔ эти решения будет проверять ваш ИТ-администратор.</span><span class="sxs-lookup"><span data-stu-id="47cfd-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="47cfd-169">✔ можно вернуться на страницу **"Публикация",** чтобы проверить состояние отправки и узнать, было ли ваше приложение утверждено или отклонено ИТ-администратором. Кроме того, здесь вы будете отправлять обновления в приложение или отменять все активные отправки.</span><span class="sxs-lookup"><span data-stu-id="47cfd-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47cfd-170">Следующий шаг: обслуживание и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="47cfd-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
