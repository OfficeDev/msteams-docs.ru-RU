---
title: Создание приложений с помощью Teams набор средств и Visual Studio
description: Начало создания больших пользовательских приложений непосредственно в Visual Studio с Microsoft Teams набор средств
keywords: набор инструментов для визуальной студии teams
localization_priority: Normal
ms.topic: overview
ms.author: johmil
ms.openlocfilehash: 6a0f466ba0d95312695be8b5460fc949e3f70811
ms.sourcegitcommit: 4ac93d69927791a8ccf678ca5ee83e63b51566b4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/23/2021
ms.locfileid: "53095516"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="ebf4f-104">Создание приложений с помощью Teams набор средств и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ebf4f-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="ebf4f-105">Набор средств Microsoft Teams Toolkit позволяет создавать пользовательские приложения Teams непосредственно в интегрированной среде разработки (IDE) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="ebf4f-106">Этот набор средств Microsoft Teams предоставит вам пошаговые инструкции в процессе создания приложения, а также все необходимое для сборки, отладки и запуска вашего приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebf4f-107">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="ebf4f-107">Prerequisites</span></span>

1. <span data-ttu-id="ebf4f-108">[Включить предварительный просмотр разработчика.](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)</span><span class="sxs-lookup"><span data-stu-id="ebf4f-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

2. <span data-ttu-id="ebf4f-109">Убедитесь, что **<span>ASP.NET</span>** и модуль веб-разработки был добавлен в экземпляр Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-109">Make sure that the **<span>ASP.NET</span> and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="ebf4f-110">Дополнительные сведения см. в [Visual Studio изменения, добавляя](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)или удаляя рабочие нагрузки и компоненты.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-110">For more information, see [Modify Visual Studio by adding or removing workloads and components](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true).</span></span>

![Модуль visual studio asp.net](../assets/images/visual-studio-web-dev-module.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="ebf4f-112">Установка Teams набор средств</span><span class="sxs-lookup"><span data-stu-id="ebf4f-112">Install the Teams Toolkit</span></span>

<span data-ttu-id="ebf4f-113">Приложение Microsoft Teams набор средств для Visual Studio доступно для скачивания с [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit) или непосредственно  из меню Расширения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-113">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="use-the-toolkit"></a><span data-ttu-id="ebf4f-114">Использование набора средств</span><span class="sxs-lookup"><span data-stu-id="ebf4f-114">Use the toolkit</span></span>

- [<span data-ttu-id="ebf4f-115">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="ebf4f-115">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="ebf4f-116">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="ebf4f-116">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="ebf4f-117">Запустите приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="ebf4f-117">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="ebf4f-118">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="ebf4f-118">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="ebf4f-119">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="ebf4f-119">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="ebf4f-120">Настройка нового проекта Teams</span><span class="sxs-lookup"><span data-stu-id="ebf4f-120">Set up a new Teams project</span></span>

1. <span data-ttu-id="ebf4f-121">Запуск Visual Studio 2019 г.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-121">Launch Visual Studio 2019.</span></span>
2. <span data-ttu-id="ebf4f-122">Выберите **Создание нового проекта.**</span><span class="sxs-lookup"><span data-stu-id="ebf4f-122">Select **Create a new project**.</span></span>
3. <span data-ttu-id="ebf4f-123">Поиск приложения **Microsoft Teams и** выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-123">Search for **Microsoft Teams App** and select **Next**.</span></span>
4. <span data-ttu-id="ebf4f-124">В **настройках нового проекта** **введите** имя Project , **Расположение** и **имя решения**.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-124">In the **Configure your new project**, enter the **Project name**, **Location**, and **Solution name**.</span></span>
5. <span data-ttu-id="ebf4f-125">Выберите **Далее,** чтобы ввести имя приложения.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-125">Select **Next** to enter a name for the app.</span></span>
6. <span data-ttu-id="ebf4f-126">На экране Дополнительные сведения введите  **имя приложения** и имя разработчика или компании для Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-126">In the Additional Information screen, enter an **Application Name** and **Developer or Company name** for your Teams app.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="ebf4f-127">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="ebf4f-127">Configure your app</span></span>

<span data-ttu-id="ebf4f-128">В основе приложения Teams три компонента:</span><span class="sxs-lookup"><span data-stu-id="ebf4f-128">At its core, the Teams app embraces three components:</span></span>

- <span data-ttu-id="ebf4f-129">Клиент Microsoft Teams (веб-, настольный или мобильный), где пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-129">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
- <span data-ttu-id="ebf4f-130">Сервер, который отвечает на запросы о контенте, отображаемом в Teams.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-130">A server that responds to requests for content displayed in Teams.</span></span> <span data-ttu-id="ebf4f-131">Например, содержимое htmL-вкладок или адаптивная карта бота.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-131">For example, HTML tab content or a bot adaptive card.</span></span>
- <span data-ttu-id="ebf4f-132">Пакет Teams состоит из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="ebf4f-132">A Teams app package consists of three files:</span></span>

    > [!div class="checklist"]
    >
    > - <span data-ttu-id="ebf4f-133">В manifest.js</span><span class="sxs-lookup"><span data-stu-id="ebf4f-133">The manifest.json</span></span>
    > - <span data-ttu-id="ebf4f-134">Значок [цвета](../resources/schema/manifest-schema.md#icons) для отображения приложения в каталоге общедоступных или организаций.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-134">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
    > - <span data-ttu-id="ebf4f-135">Значок [плана](../resources/schema/manifest-schema.md#icons) для отображения на панели Teams действий.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-135">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="ebf4f-136">При установке приложения клиент Teams определяет файл манифеста, чтобы определить необходимые сведения, такие как имя приложения и URL-адрес, в котором находятся службы.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-136">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="ebf4f-137">Если вы еще этого не сделали, необходимо войти в Microsoft 365 учетную запись, чтобы продолжить процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-137">If you have not done so already, you must sign in to your Microsoft 365 account to continue with the development process.</span></span>
>
> <span data-ttu-id="ebf4f-138">Если у вас нет Microsoft 365 учетной записи, вы можете подписаться на подписку [Microsoft 365 разработчика.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="ebf4f-138">If you do not have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="ebf4f-139">Он бесплатный в течение 90 дней и обновляется до тех пор, пока вы используете его для разработки.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-139">It's free for 90 days and renews as long as you are using it for development activity.</span></span> <span data-ttu-id="ebf4f-140">Если у вас есть подписка Visual Studio Enterprise или Professional, обе программы включают бесплатную подписку Microsoft 365 [разработчика,](https://aka.ms/MyVisualStudioBenefits)активную для Visual Studio подписки.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-140">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="ebf4f-141">Дополнительные сведения см. [в Microsoft 365 подписки разработчика.](/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="ebf4f-141">For more information, see [set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="ebf4f-142">Этапы конфигурации</span><span class="sxs-lookup"><span data-stu-id="ebf4f-142">Configuration steps</span></span>

1. <span data-ttu-id="ebf4f-143">Чтобы настроить приложение, выберите Project > **TeamsFx > настройка для меню SSO...**</span><span class="sxs-lookup"><span data-stu-id="ebf4f-143">To configure your app, select the **Project > TeamsFx > Configure for SSO...** menu.</span></span>

<span data-ttu-id="ebf4f-144">При запросе впишитесь в свою учетную запись Майкрософт с клиентом M365.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-144">When prompted, sign in to your Microsoft account that has an M365 tenant.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="ebf4f-145">Установка и локальное запуск приложения</span><span class="sxs-lookup"><span data-stu-id="ebf4f-145">Install and run your app locally</span></span>

<span data-ttu-id="ebf4f-146">Нажмите кнопку F5, чтобы начать отладку.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-146">Press F5 to start debugging.</span></span> <span data-ttu-id="ebf4f-147">Диалоговое окно установки приложения отображается в Teams клиенте.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-147">The app installation dialog box appears in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="ebf4f-148">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="ebf4f-148">Validate your app</span></span>

<span data-ttu-id="ebf4f-149">Меню **Project > TeamsFx Validate > Teams манифеста** позволяет проверить, действителен ли ваш пакет приложений.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-149">The **Project > TeamsFx Validate > Teams Manifest** menu allows you to check that your app package is valid.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="ebf4f-150">Опубликуйте свое приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="ebf4f-150">Publish your app to Teams</span></span>

<span data-ttu-id="ebf4f-151">На [портале Teams](https://dev.teams.microsoft.com/home)разработчиков вы можете загрузить приложение в команду, отправить приложение в пользовательский магазин приложений для пользователей вашей организации или отправить приложение в App Source для всех Teams пользователей.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-151">In the [Teams Developer Portal](https://dev.teams.microsoft.com/home), you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

- <span data-ttu-id="ebf4f-152">ИТ-администратор проверит эти отправленные приложения.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-152">Your IT admin will review these submissions.</span></span>
- <span data-ttu-id="ebf4f-153">Вы можете вернуться на страницу **Публикация,** чтобы проверить состояние отправки и узнать, было ли ваше приложение утверждено или отклонено вашим ИТ-администратором. Здесь также можно отправлять обновления в приложение или отменять активные в настоящее время отправки.</span><span class="sxs-lookup"><span data-stu-id="ebf4f-153">You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you can submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="ebf4f-154">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="ebf4f-154">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ebf4f-155">Создание и запуск первого Microsoft Teams приложения с помощью Blazor</span><span class="sxs-lookup"><span data-stu-id="ebf4f-155">Build and run your first Microsoft Teams app with Blazor</span></span>](../get-started/first-app-blazor.md)
