---
title: Создание приложений с помощью набора инструментов Microsoft Teams и Visual Studio
description: Приступая к созданию привлекательных пользовательских приложений непосредственно в Visual Studio с помощью набора инструментов Microsoft Teams
keywords: набор средств Visual Studio для Teams
ms.date: 06/30/2020
ms.openlocfilehash: e5715cf23cfd221b65afe0e6258ce06ff98770aa
ms.sourcegitcommit: 694babb79d379360a20cf928a9d2b88dd6d3bdd0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/07/2020
ms.locfileid: "45051720"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a><span data-ttu-id="5aee2-104">Создание приложений с помощью набора инструментов Microsoft Teams и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5aee2-104">Build apps with the Microsoft Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="5aee2-105">Набор средств Microsoft Teams позволяет создавать пользовательские приложения Teams непосредственно в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5aee2-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio environment.</span></span> <span data-ttu-id="5aee2-106">Набор средств поможет вам выполнить все действия, необходимые для создания, отладки и запуска приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="5aee2-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="5aee2-107">Установка набора инструментов Teams</span><span class="sxs-lookup"><span data-stu-id="5aee2-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="5aee2-108">Набор средств Microsoft Teams для Visual Studio можно загрузить из [Visual Studio Marketplace](https://aka.ms/teams-toolkit) или напрямую как расширение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5aee2-108">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="5aee2-109">Использование набора средств</span><span class="sxs-lookup"><span data-stu-id="5aee2-109">Using the toolkit</span></span>

- [<span data-ttu-id="5aee2-110">Настройка нового проекта</span><span class="sxs-lookup"><span data-stu-id="5aee2-110">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="5aee2-111">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="5aee2-111">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="5aee2-112">Упаковка приложения</span><span class="sxs-lookup"><span data-stu-id="5aee2-112">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="5aee2-113">Запуск приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="5aee2-113">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="5aee2-114">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="5aee2-114">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="5aee2-115">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="5aee2-115">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="5aee2-116">Настройка нового проекта Teams</span><span class="sxs-lookup"><span data-stu-id="5aee2-116">Set up a new Teams project</span></span>

1. <span data-ttu-id="5aee2-117">Создайте новый проект и выберите шаблон Microsoft Терамс Toolkit.</span><span class="sxs-lookup"><span data-stu-id="5aee2-117">Create a new project and select the Microsoft Terams Toolkit template.</span></span>
1. <span data-ttu-id="5aee2-118">Вы будете поступать на экране **Add Capabilities (добавить возможности** ), чтобы настроить свойства нового приложения.</span><span class="sxs-lookup"><span data-stu-id="5aee2-118">You will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="5aee2-119">Нажмите кнопку **Готово** , чтобы завершить процесс настройки.</span><span class="sxs-lookup"><span data-stu-id="5aee2-119">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="5aee2-120">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="5aee2-120">Configure your app</span></span>

<span data-ttu-id="5aee2-121">В основном приложение Teams поработает с тремя компонентами:</span><span class="sxs-lookup"><span data-stu-id="5aee2-121">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="5aee2-122">Клиент Microsoft Teams (веб-сайт, Настольный компьютер или мобильное устройство), на котором пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="5aee2-122">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="5aee2-123">Сервер, который отвечает на запросы для контента, который будет отображаться в Teams, например, контент вкладки HTML или адаптивной карточки Bot.</span><span class="sxs-lookup"><span data-stu-id="5aee2-123">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="5aee2-124">[Пакет приложения](/concepts/build-and-test/apps-package.md) Teams состоит из трех файлов:</span><span class="sxs-lookup"><span data-stu-id="5aee2-124">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="5aee2-125">manifest.jsна</span><span class="sxs-lookup"><span data-stu-id="5aee2-125">The manifest.json</span></span> 
  > - <span data-ttu-id="5aee2-126">[Значок цвета](../resources/schema/manifest-schema.md#icons) приложения для отображения в каталоге приложений "общедоступный" или "Организация"</span><span class="sxs-lookup"><span data-stu-id="5aee2-126">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="5aee2-127">[Значок структуры](../resources/schema/manifest-schema.md#icons) для отображения на панели активности Teams.</span><span class="sxs-lookup"><span data-stu-id="5aee2-127">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="5aee2-128">При установке приложения клиент Teams анализирует файл манифеста, чтобы определить необходимые сведения, такие как имя вашего приложения и URL-адрес, по которому расположены службы.</span><span class="sxs-lookup"><span data-stu-id="5aee2-128">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="5aee2-129">Чтобы настроить приложение, перейдите в окно расширения **набора средств Microsoft Teams** .</span><span class="sxs-lookup"><span data-stu-id="5aee2-129">To configure your app, navigate to the **Microsoft Teams Toolkit** extension window.</span></span>
1. <span data-ttu-id="5aee2-130">Выберите команду **изменить пакет приложения** , чтобы просмотреть страницу **сведений о приложении** .</span><span class="sxs-lookup"><span data-stu-id="5aee2-130">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="5aee2-131">Изменение полей на странице "сведения о приложении" обновляет содержимое manifest.jsв файле, который в конечном итоге будет поставляться в составе пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="5aee2-131">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="5aee2-132">Подробнее</span><span class="sxs-lookup"><span data-stu-id="5aee2-132">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="5aee2-133">Упаковка приложения</span><span class="sxs-lookup"><span data-stu-id="5aee2-133">Package your app</span></span>

<span data-ttu-id="5aee2-134">Изменение страницы **сведений о приложении** или обновление **манифеста**, или **env** -файлов в папке **публикации** приложения автоматически создаст файл **Development.zip** .</span><span class="sxs-lookup"><span data-stu-id="5aee2-134">Modifying your the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="5aee2-135">Необходимо включить [два значка](../concepts/build-and-test/apps-package.md#icons) в одну и ту же папку.</span><span class="sxs-lookup"><span data-stu-id="5aee2-135">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="5aee2-136">Установка и запуск приложения на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="5aee2-136">Install and run your app locally</span></span>

<span data-ttu-id="5aee2-137">В раскрывающемся меню *конфигурации решений* выберите команду *развернуть*.</span><span class="sxs-lookup"><span data-stu-id="5aee2-137">From the *Solutions Configurations* dropdown menu, select *Deploy*.</span></span> <span data-ttu-id="5aee2-138">Нажмите кнопку *ISS Express + Teams* .</span><span class="sxs-lookup"><span data-stu-id="5aee2-138">Press the *ISS Express + Teams* button.</span></span> <span data-ttu-id="5aee2-139">Запускаются Teams, а диалоговое окно установки приложения должно отображаться в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="5aee2-139">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="5aee2-140">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="5aee2-140">Validate your app</span></span>

<span data-ttu-id="5aee2-141">Страница **проверки** позволяет проверить пакет приложения перед отправкой приложения в AppSource.</span><span class="sxs-lookup"><span data-stu-id="5aee2-141">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="5aee2-142">Просто отправьте пакет манифеста, и средство проверки проверит ваше приложение на соответствие всем тестовым случаям, связанным с манифестом.</span><span class="sxs-lookup"><span data-stu-id="5aee2-142">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="5aee2-143">Для каждого неудачных тестов в описании представлена ссылка на документацию, которая поможет исправить ошибку.</span><span class="sxs-lookup"><span data-stu-id="5aee2-143">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="5aee2-144">Для тестов, которые трудно автоматизировать, **Предварительный контрольный список** включает 7 наиболее распространенных тестовых случаев, а также ссылки на полный контрольный список отправки.</span><span class="sxs-lookup"><span data-stu-id="5aee2-144">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="5aee2-145">Публикация приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="5aee2-145">Publish your app to Teams</span></span>

<span data-ttu-id="5aee2-146">На домашней странице проекта вы можете отправить свое приложение в группу, отправить свое приложение в пользовательскую магазин приложений для пользователей в вашей организации или отправить свое приложение в источник приложений для всех пользователей Teams.</span><span class="sxs-lookup"><span data-stu-id="5aee2-146">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="5aee2-147">ИТ ИТ ИТ, просматривая эти отправки.</span><span class="sxs-lookup"><span data-stu-id="5aee2-147">Your IT admin will review these submissions.</span></span> <span data-ttu-id="5aee2-148">Вы можете вернуться на страницу *публикации* , чтобы проверить состояние отправки, а также узнать, было ли ваше приложение утверждено или отклонено вашим ИТ-администратором. Кроме того, здесь вы будете передавать обновления в свое приложение или отменять все активные в данный момент отправки.</span><span class="sxs-lookup"><span data-stu-id="5aee2-148">You can return to the *Publish* page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5aee2-149">Следующий шаг: обслуживание и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="5aee2-149">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
