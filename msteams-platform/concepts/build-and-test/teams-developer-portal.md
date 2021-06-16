---
title: Управление приложениями с помощью портала разработчиков
description: Узнайте, как управлять приложениями с помощью портала разработчиков для Microsoft Teams.
keywords: начало работы команд портала разработчиков
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 6dca8723248441c3cf672931295b4b68e02cc24c
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949688"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a><span data-ttu-id="51965-104">Управление приложениями с помощью портала разработчиков для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="51965-104">Manage your apps with the Developer Portal for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="51965-105">Портал разработчика для Teams в настоящее время находится в [предварительном просмотре общедоступных разработчиков.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="51965-105">The Developer Portal for Teams is currently in [public developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

<span data-ttu-id="51965-106">Портал <a href="https://dev.teams.microsoft.com" target="_blank">разработчиков для Teams</a> является основным средством настройки, распространения и управления Microsoft Teams приложениями.</span><span class="sxs-lookup"><span data-stu-id="51965-106">The <a href="https://dev.teams.microsoft.com" target="_blank">Developer Portal for Teams</a> is the primary tool for configuring, distributing, and managing your Microsoft Teams apps.</span></span> <span data-ttu-id="51965-107">На портале разработчиков вы можете сотрудничать с коллегами в вашем приложении, настроить среды запуска и многое другое.</span><span class="sxs-lookup"><span data-stu-id="51965-107">With the Developer Portal, you can collaborate with colleagues on your app, set up runtime environments, and much more.</span></span>

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="Снимок экрана, на котором показана главная страница портала разработчиков для Teams.":::

## <a name="register-an-app"></a><span data-ttu-id="51965-109">Регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="51965-109">Register an app</span></span>

<span data-ttu-id="51965-110">Портал разработчика предоставляет несколько способов регистрации Teams приложения:</span><span class="sxs-lookup"><span data-stu-id="51965-110">The Developer Portal provides a couple ways to register a Teams app:</span></span>

* <span data-ttu-id="51965-111">Регистрация нового приложения</span><span class="sxs-lookup"><span data-stu-id="51965-111">Register a brand new app</span></span>
* <span data-ttu-id="51965-112">Импорт существующего пакета приложений</span><span class="sxs-lookup"><span data-stu-id="51965-112">Import an existing app package</span></span>

> [!NOTE]
> <span data-ttu-id="51965-113">Если вы создаете приложение с Microsoft Teams набор средств [для Visual Studio Code,](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)вы можете управлять этим приложением на портале разработчиков.</span><span class="sxs-lookup"><span data-stu-id="51965-113">If you create an app using the [Microsoft Teams Toolkit for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension), you can manage that app in the Developer Portal.</span></span>

## <a name="set-up-an-environment"></a><span data-ttu-id="51965-114">Настройка среды</span><span class="sxs-lookup"><span data-stu-id="51965-114">Set up an environment</span></span>

<span data-ttu-id="51965-115">Вы можете настроить среды и глобальные переменные, чтобы помочь вашему приложению перейти из локального времени работы в производство.</span><span class="sxs-lookup"><span data-stu-id="51965-115">You can configure environments and global variables to help transition your app from your local runtime to production.</span></span> <span data-ttu-id="51965-116">Глобальные переменные используются во всех средах.</span><span class="sxs-lookup"><span data-stu-id="51965-116">Global variables are used across all environments.</span></span>

<span data-ttu-id="51965-117">**Настройка среды**</span><span class="sxs-lookup"><span data-stu-id="51965-117">**To set up an environment**</span></span>

1. <span data-ttu-id="51965-118">На портале разработчиков выберите приложение, над которое работаете.</span><span class="sxs-lookup"><span data-stu-id="51965-118">In the Developer Portal, select the app you're working on.</span></span>
2. <span data-ttu-id="51965-119">Перейдите на **страницу Среды** и выберите **+ Добавить среду.**</span><span class="sxs-lookup"><span data-stu-id="51965-119">Go to the **Environments** page and select **+ Add an environment**.</span></span>
3. <span data-ttu-id="51965-120">Выберите **+ Добавьте переменную для** создания переменных конфигурации для среды.</span><span class="sxs-lookup"><span data-stu-id="51965-120">Select **+ Add a variable** to create configuration variables for your environment.</span></span>

<span data-ttu-id="51965-121">**Использование переменных**</span><span class="sxs-lookup"><span data-stu-id="51965-121">**To use variables**</span></span>

<span data-ttu-id="51965-122">Для настройки конфигураций приложений используйте имена переменных вместо значений с жесткой кодом.</span><span class="sxs-lookup"><span data-stu-id="51965-122">Use the variable names instead of hard-coded values to set your app configurations.</span></span>

1. <span data-ttu-id="51965-123">Введите `{{` в любом поле портал разработчика.</span><span class="sxs-lookup"><span data-stu-id="51965-123">Enter `{{` in any field in the Developer Portal.</span></span> <span data-ttu-id="51965-124">Появляется отсев со всеми переменными, созданными для выбранной среды, а также глобальными переменными.</span><span class="sxs-lookup"><span data-stu-id="51965-124">A dropdown with all the variables you've created for the chosen environment along with the global variables appears.</span></span>  
1. <span data-ttu-id="51965-125">Перед скачиванием пакета приложений (например, при готовке к публикации в Teams магазине) выберите среду, в которой вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="51965-125">Before downloading your app package (for example, when getting ready to publish to the Teams store), select the environment you want to use.</span></span> <span data-ttu-id="51965-126">Конфигурации приложений обновляются автоматически в зависимости от среды.</span><span class="sxs-lookup"><span data-stu-id="51965-126">Your app configurations update automatically based on the environment.</span></span> 

## <a name="identify-app-owners"></a><span data-ttu-id="51965-127">Определение владельцев приложений</span><span class="sxs-lookup"><span data-stu-id="51965-127">Identify app owners</span></span>

<span data-ttu-id="51965-128">Каждое приложение включает страницу **Owners,** на которой вы можете поделиться регистрацией приложения с коллегами в вашей организации. Роль **Contributor** имеет те же разрешения, что и роль **Владельца,** за исключением возможности удаления приложения.</span><span class="sxs-lookup"><span data-stu-id="51965-128">Each app includes an **Owners** page, where you can share your app registration with colleagues in your org. The **Contributor** role has the same permissions as the **Owner** role except the ability to delete an app.</span></span>

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a><span data-ttu-id="51965-129">Настройка возможностей приложения и других важных метаданных</span><span class="sxs-lookup"><span data-stu-id="51965-129">Configure your app's capabilities and other important metadata</span></span>

<span data-ttu-id="51965-130">Приложение Teams — это веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="51965-130">A Teams app is a web app.</span></span> <span data-ttu-id="51965-131">Как и все веб-приложения, его исходный код обычно разрабатывается в редакторе IDE или кода и находится где-то в облаке (например, в Azure).</span><span class="sxs-lookup"><span data-stu-id="51965-131">Like all web apps, its source code is typically developed in an IDE or code editor and hosted somewhere in the cloud (like Azure).</span></span>

<span data-ttu-id="51965-132">Чтобы установить и отрисовка приложения в Teams, необходимо включить набор конфигураций, Teams распознает.</span><span class="sxs-lookup"><span data-stu-id="51965-132">To install and render your app in Teams, you must include a set of configurations that Teams recognizes.</span></span> <span data-ttu-id="51965-133">Это традиционно делается путем с помощью манифеста приложения — JSON-файла, который содержит все метаданные Teams необходимые для отображения контента приложения.</span><span class="sxs-lookup"><span data-stu-id="51965-133">This has traditionally been done by crafting an app manifest, a JSON file that contains all the metadata Teams needs to display your app content.</span></span> <span data-ttu-id="51965-134">Портал разработчиков абстрагировать этот процесс и включает новые функции и средства, которые помогут вам быть более успешными.</span><span class="sxs-lookup"><span data-stu-id="51965-134">The Developer Portal abstracts this process and includes new features and tooling to help you be more successful.</span></span>

## <a name="test-your-app-directly-in-teams"></a><span data-ttu-id="51965-135">Тестирование приложения непосредственно в Teams</span><span class="sxs-lookup"><span data-stu-id="51965-135">Test your app directly in Teams</span></span>

<span data-ttu-id="51965-136">Портал разработчиков предоставляет варианты тестирования и отладки приложения:</span><span class="sxs-lookup"><span data-stu-id="51965-136">The Developer Portal provides options for testing and debugging your app:</span></span>

* <span data-ttu-id="51965-137">На странице **Обзор** можно увидеть снимок проверки конфигураций вашего приложения Teams тестовых случаях.</span><span class="sxs-lookup"><span data-stu-id="51965-137">On the **Overview** page, you can see a snapshot of whether your app's configurations validate against Teams store test cases.</span></span>
* <span data-ttu-id="51965-138">Кнопка **Preview Teams** позволяет быстро запустить приложение в клиенте Teams для отладки.</span><span class="sxs-lookup"><span data-stu-id="51965-138">The **Preview in Teams** button lets you launch your app quickly in the Teams client for debugging.</span></span>

## <a name="distribute-your-app"></a><span data-ttu-id="51965-139">Распространение приложения</span><span class="sxs-lookup"><span data-stu-id="51965-139">Distribute your app</span></span>

<span data-ttu-id="51965-140">На портале разработчиков используйте кнопку **"Распространение"** для скачивания пакета приложений, публикации на сайте организации или публикации в Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="51965-140">From the Developer Portal, use the **Distribute** button to download an app package, publish to your org, or publish to the Teams store.</span></span>

<span data-ttu-id="51965-141">Дополнительные сведения см. в [Teams приложения.](~/concepts/deploy-and-publish/apps-publish-overview.md)</span><span class="sxs-lookup"><span data-stu-id="51965-141">For more information, see [distribute your Teams app](~/concepts/deploy-and-publish/apps-publish-overview.md).</span></span>

## <a name="analyze-your-apps-usage"></a><span data-ttu-id="51965-142">Анализ использования приложения</span><span class="sxs-lookup"><span data-stu-id="51965-142">Analyze your app's usage</span></span>

<span data-ttu-id="51965-143">На странице **Обзор** можно увидеть общее число активных пользователей для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="51965-143">On the **Overview** page, you can see the total number of active users for your app.</span></span> <span data-ttu-id="51965-144">Эти показатели доступны для приложений, опубликованных в Teams магазине или каталоге приложений организации через портал разработчика и в области для ID приложения.</span><span class="sxs-lookup"><span data-stu-id="51965-144">These metrics are available for apps published to the Teams store or an org's app catalog through Developer Portal and scoped to the app ID.</span></span>

| <span data-ttu-id="51965-145">Метрика</span><span class="sxs-lookup"><span data-stu-id="51965-145">Metric</span></span> | <span data-ttu-id="51965-146">Определение</span><span class="sxs-lookup"><span data-stu-id="51965-146">Definition</span></span> |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="51965-147">*Ежемесячный R30*</span><span class="sxs-lookup"><span data-stu-id="51965-147">*Monthly R30*</span></span> | <span data-ttu-id="51965-148">Показатель использования по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="51965-148">The default usage metric.</span></span> <span data-ttu-id="51965-149">В нем показано количество уникальных активных пользователей, которые использовали ваше приложение в этом 30-дневном окне UTC.</span><span class="sxs-lookup"><span data-stu-id="51965-149">It shows you the count of unique active users that used your app within that rolling 30-day window in UTC.</span></span> |
| <span data-ttu-id="51965-150">*Daily (Ежедневный)*</span><span class="sxs-lookup"><span data-stu-id="51965-150">*Daily*</span></span> | <span data-ttu-id="51965-151">Показывает количество уникальных активных пользователей, которые использовали ваше приложение в данный день в UTC.</span><span class="sxs-lookup"><span data-stu-id="51965-151">Shows you the count of unique active users that used your app in a given day in UTC.</span></span> |

<span data-ttu-id="51965-152">Ежемесячное и ежедневное использование отображается в течение последних 7, 30 дней и 60 дней.</span><span class="sxs-lookup"><span data-stu-id="51965-152">Monthly and daily usage is shown for the past seven, 30 days, and 60 days.</span></span> <span data-ttu-id="51965-153">В течение 24-48 часов следует увидеть использование, отражаемого в течение данного дня.</span><span class="sxs-lookup"><span data-stu-id="51965-153">You should see usage reflected for a given day within 24-48 hours.</span></span> <span data-ttu-id="51965-154">Использование новых приложений может занять до 3-5 дней.</span><span class="sxs-lookup"><span data-stu-id="51965-154">Usage for new apps can take up to 3-5 days to display.</span></span>

## <a name="use-tools-to-create-app-features"></a><span data-ttu-id="51965-155">Использование инструментов для создания функций приложения</span><span class="sxs-lookup"><span data-stu-id="51965-155">Use tools to create app features</span></span>

<span data-ttu-id="51965-156">Портал разработчиков также включает средства, которые помогут вам создать некоторые ключевые функции Teams приложений.</span><span class="sxs-lookup"><span data-stu-id="51965-156">The Developer Portal also includes tools to help you build some key features of Teams apps.</span></span> <span data-ttu-id="51965-157">Некоторые из этих средств включают в себя:</span><span class="sxs-lookup"><span data-stu-id="51965-157">Some of these tools include:</span></span>

* <span data-ttu-id="51965-158">**Сцена студии**: [Разработка настраиваемой совместной](~/apps-in-teams-meetings/teams-together-mode.md) сцены режима для Teams собраний.</span><span class="sxs-lookup"><span data-stu-id="51965-158">**Scene studio**: Design [custom Together Mode scenes](~/apps-in-teams-meetings/teams-together-mode.md) for Teams meetings.</span></span>
* <span data-ttu-id="51965-159">**Редактор адаптивных карт.** Создание и предварительный просмотр адаптивных карт, чтобы включить их в приложения.</span><span class="sxs-lookup"><span data-stu-id="51965-159">**Adaptive Cards editor**: Create and preview Adaptive Cards to include with your apps.</span></span>
* <span data-ttu-id="51965-160">**платформа удостоверений Майкрософт** управления. Зарегистрируйте свои приложения Azure Active Directory (Azure AD), чтобы помочь пользователям войти и предоставить доступ к API.</span><span class="sxs-lookup"><span data-stu-id="51965-160">**Microsoft identity platform management**: Register your apps with Azure Active Directory (Azure AD) to help users sign in and provide access to APIs.</span></span>
