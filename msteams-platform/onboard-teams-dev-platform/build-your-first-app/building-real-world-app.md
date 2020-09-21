---
title: Приступая к созданию первого приложения Teams
author: heath-hamilton
ms.author: lajanuar
description: Обзор и предварительные требования для создания первого приложения Microsoft Teams
ms.openlocfilehash: 9392096a285a43d3a1f8bed5020e3464da0f7f18
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964765"
---
# <a name="get-started-building-your-first-teams-app"></a><span data-ttu-id="834c6-103">Приступая к созданию первого приложения Teams</span><span class="sxs-lookup"><span data-stu-id="834c6-103">Get started building your first Teams app</span></span>

<span data-ttu-id="834c6-104">В разделе **Создание первых** приложений вы создадите базовые приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="834c6-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="834c6-105">В каждом учебном курсе описывается создание простого приложения Teams, а также общие инструменты, основные понятия и некоторые дополнительные возможности.</span><span class="sxs-lookup"><span data-stu-id="834c6-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and some more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="834c6-106">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="834c6-106">What you'll learn</span></span>

<span data-ttu-id="834c6-107">Ниже представлены сведения о том, что вы узнаете после изучения уроков.</span><span class="sxs-lookup"><span data-stu-id="834c6-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="834c6-108">**Быстрый запуск и работа с набором инструментов Teams**: набор инструментов Microsoft Teams для Visual Studio Code создает проект приложения и формирование шаблонов, чтобы приложение могло работать в минутах.</span><span class="sxs-lookup"><span data-stu-id="834c6-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="834c6-109">**Определите приложение с манифестом**: в манифесте приложения указываются возможности и службы, которые использует приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="834c6-109">**Define your app with the manifest**: The app manifest is where you specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="834c6-110">**Область аудиторий приложения**: создание приложения Teams для личного использования, совместной работы или и того, и другое.</span><span class="sxs-lookup"><span data-stu-id="834c6-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
  > * <span data-ttu-id="834c6-111">**Знакомство с платформами**: Настройка приложения (например, изменение цветовой схемы для согласования с темой Teams) с помощью справки из пакета SDK для Teams.</span><span class="sxs-lookup"><span data-stu-id="834c6-111">**Get experience with frameworks**: Customize your app (for example, change its color scheme to match the Teams theme) with help from the Teams JavaScript SDK.</span></span> <span data-ttu-id="834c6-112">Кроме того, Узнайте о стандартных средствах для создания и управления Боты.</span><span class="sxs-lookup"><span data-stu-id="834c6-112">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="834c6-113">**Разверните приложение на своем приложении**: в уроках вы найдете связанные темы (например, рекомендации по проверке подлинности и проектированию).</span><span class="sxs-lookup"><span data-stu-id="834c6-113">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="834c6-114">Основные сведения о приложениях Teams</span><span class="sxs-lookup"><span data-stu-id="834c6-114">Teams app fundamentals</span></span>

<span data-ttu-id="834c6-115">Прежде чем приступать к работе с руководствами, необходимо знать следующее о создании приложений для Teams.</span><span class="sxs-lookup"><span data-stu-id="834c6-115">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities"></a><span data-ttu-id="834c6-116">Приложения могут иметь несколько возможностей</span><span class="sxs-lookup"><span data-stu-id="834c6-116">Apps can have multiple capabilities</span></span>

<span data-ttu-id="834c6-117">Приложения Teams состоят из одной или нескольких [функций платформы](../capabilities-overview.md).</span><span class="sxs-lookup"><span data-stu-id="834c6-117">Teams apps are made up of one or more [platform capabilities](../capabilities-overview.md).</span></span> <span data-ttu-id="834c6-118">Эти возможности можно отобразить с помощью ряда [компонентов пользовательского интерфейса](../doc-links/teams-ui-conventions.md), определенных для Teams, а также соглашений, таких как карточки и модули задач.</span><span class="sxs-lookup"><span data-stu-id="834c6-118">You can display these capabilities using a number of Teams-specific [UI components and conventions](../doc-links/teams-ui-conventions.md), such as cards and task modules.</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="834c6-119">В Teams не размещается ваше приложение</span><span class="sxs-lookup"><span data-stu-id="834c6-119">Teams doesn't host your app</span></span>

<span data-ttu-id="834c6-120">Приложение Teams включает три важных этапа:</span><span class="sxs-lookup"><span data-stu-id="834c6-120">A Teams app includes three important pieces:</span></span>

* <span data-ttu-id="834c6-121">Логика, хранилище данных и вызовы API, которые переключают приложение.</span><span class="sxs-lookup"><span data-stu-id="834c6-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="834c6-122">Эти службы не размещаются в Teams и должны быть доступны по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="834c6-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="834c6-123">Клиент Teams (на веб-сайте, на настольном компьютере или мобильном устройстве), в котором пользователи используют ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="834c6-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="834c6-124">Ваш пакет приложения, который вы используете для установки приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="834c6-124">Your app package, which you use to install the app in Teams.</span></span> <span data-ttu-id="834c6-125">Он содержит метаданные приложения и указатели на размещенные службы.</span><span class="sxs-lookup"><span data-stu-id="834c6-125">It contains app metadata and pointers to your hosted services.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="834c6-126">Получение необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="834c6-126">Get prerequisites</span></span>

<span data-ttu-id="834c6-127">Убедитесь, что у вас есть правильная учетная запись для создания приложений Teams и установки некоторых рекомендуемых средств разработки.</span><span class="sxs-lookup"><span data-stu-id="834c6-127">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="834c6-128">Настройка учетной записи для разработки</span><span class="sxs-lookup"><span data-stu-id="834c6-128">Set up your development account</span></span>

<span data-ttu-id="834c6-129">Вам нужна учетная запись Teams, которая разрешает нестандартную загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="834c6-129">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="834c6-130">(Это может быть уже предоставлено вашей учетной записью.)</span><span class="sxs-lookup"><span data-stu-id="834c6-130">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="834c6-131">Если у вас есть учетная запись Teams, убедитесь, что вы можете Загрузка неопубликованных приложения в teams:</span><span class="sxs-lookup"><span data-stu-id="834c6-131">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="834c6-132">В клиенте Teams выберите **приложения**.</span><span class="sxs-lookup"><span data-stu-id="834c6-132">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="834c6-133">Найдите параметр для **отправки настраиваемого приложения**.</span><span class="sxs-lookup"><span data-stu-id="834c6-133">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../doc-links/images/upload-custom-app-closeup.png" alt-text="режим Загрузка неопубликованных":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="834c6-135">Если вы не видите параметр Загрузка неопубликованных или у вас нет учетной записи Teams, <b>выберите здесь</b> .</span><span class="sxs-lookup"><span data-stu-id="834c6-135"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="834c6-136">Вы можете получить бесплатную тестовую учетную запись Teams, позволяющую выполнять загрузку неопубликованных приложений, присоединяясь к программе для разработчиков Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="834c6-136">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="834c6-137">(Процесс регистрации занимает около двух минут.)</span><span class="sxs-lookup"><span data-stu-id="834c6-137">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="834c6-138">Перейдите к [программе для разработчиков Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="834c6-138">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="834c6-139">Нажмите кнопку **присоединиться сейчас** и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="834c6-139">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="834c6-140">При получении экрана приветствия выберите пункт **настроить подписку**по клавише вверх.</span><span class="sxs-lookup"><span data-stu-id="834c6-140">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="834c6-141">Настройте учетную запись администратора.</span><span class="sxs-lookup"><span data-stu-id="834c6-141">Set up your administrator account.</span></span> <span data-ttu-id="834c6-142">После завершения вы увидите экран следующего вида:</span><span class="sxs-lookup"><span data-stu-id="834c6-142">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../doc-links/images/dev-program-subscription.png" alt-text="представление подписки по программе для разработчиков":::
1. <span data-ttu-id="834c6-144">Войдите в Teams с помощью учетной записи администратора, которую вы только что настроили.</span><span class="sxs-lookup"><span data-stu-id="834c6-144">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="834c6-145">Убедитесь, что у вас теперь есть параметр **Отправить настраиваемое приложение** .</span><span class="sxs-lookup"><span data-stu-id="834c6-145">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

### <a name="install-your-development-tools"></a><span data-ttu-id="834c6-146">Установка средств разработки</span><span class="sxs-lookup"><span data-stu-id="834c6-146">Install your development tools</span></span>

<span data-ttu-id="834c6-147">Вы можете создавать приложения Teams с помощью своих предпочтительных средств, но на этих занятиях показано, как быстро начать работу с набором инструментов Microsoft Teams для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="834c6-147">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="834c6-148">Teams отображает контент приложения только через HTTPS подключения.</span><span class="sxs-lookup"><span data-stu-id="834c6-148">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="834c6-149">Так как вы размещаете свое первое приложение локально, вы узнаете, как использовать [ngrok для настройки безопасного туннеля](../doc-links/debug.md#locally-hosted) между Teams и приложением.</span><span class="sxs-lookup"><span data-stu-id="834c6-149">Since you'll host your first app locally, you'll learn how to use [ngrok to set up a secure tunnel](../doc-links/debug.md#locally-hosted) between Teams and your app.</span></span>

1. <span data-ttu-id="834c6-150">Установите [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="834c6-150">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="834c6-151">Установите последнюю версию [Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="834c6-151">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="834c6-152">(Более ранние версии могут не работать с этим набором инструментов.)</span><span class="sxs-lookup"><span data-stu-id="834c6-152">(Earlier versions might not work with the toolkit.)</span></span>
1. В Visual Studio Code выберите **расширения** :::image type="icon" source="../doc-links/images/vs-code-extensions.png"::: на левой панели действий и установите **набор инструментов Microsoft Teams**.
    :::image type="content" source="../doc-links/images/vsc-install-toolkit.png" alt-text="Установка представления набора инструментов":::
1. <span data-ttu-id="834c6-155">Установите [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="834c6-155">Install [ngrok](https://ngrok.com/download).</span></span>

## <a name="next-step"></a><span data-ttu-id="834c6-156">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="834c6-156">Next step</span></span>

<span data-ttu-id="834c6-157">После настройки учетной записи и среды можно приступить к созданию.</span><span class="sxs-lookup"><span data-stu-id="834c6-157">Once you set up your account and environment, you can start building.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="834c6-158">Создание и запуск первого приложения</span><span class="sxs-lookup"><span data-stu-id="834c6-158">Build and run your first app</span></span>](../build-your-first-app/build-and-run.md)
