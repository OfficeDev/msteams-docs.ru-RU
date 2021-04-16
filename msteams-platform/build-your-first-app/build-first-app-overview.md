---
title: Начало работы — создание первого обзора приложения и необходимых условий
author: heath-hamilton
description: Узнайте, как начать разработку приложений Microsoft Teams и настроить среду.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 6594ac175cd8ad92c5db399bb675ef3a6b271321
ms.sourcegitcommit: 0e252159f53ff9b4452e0574b759bfe73cbf6c84
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/14/2021
ms.locfileid: "51762041"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="295be-103">Создание первого обзора приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="295be-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="295be-104">На начало **занятий** вы узнаете, как создавать базовые приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="295be-104">In the **get started** lessons, you learn how to create basic Teams apps.</span></span> <span data-ttu-id="295be-105">Каждый учебник включает в себя создание простого приложения Teams с реальными возможностями, а также знакомит вас с общими средствами, фундаментальными концепциями и более продвинутыми функциями.</span><span class="sxs-lookup"><span data-stu-id="295be-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="295be-106">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="295be-106">What you'll learn</span></span>

<span data-ttu-id="295be-107">Вот представление о том, что вы узнаете после того, как будете проходить уроки.</span><span class="sxs-lookup"><span data-stu-id="295be-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="295be-108">Быстро встайте в группу **набор средств:** microsoft Teams набор средств для Visual Studio Code позаботится о создании проекта приложения и строительных лесов, чтобы у вас было запущено приложение за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="295be-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="295be-109">**Настройка приложения с помощью App Studio:** укажите возможности и службы, которые использует приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="295be-109">**Configure your app with App Studio**: Specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="295be-110">**Область аудитории приложения:** создание приложения Teams для личного использования, совместной работы или обоих.</span><span class="sxs-lookup"><span data-stu-id="295be-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
> * <span data-ttu-id="295be-111">**Получите опыт работы с средствами Teams и SDK:** настройте приложение с помощью SDK клиента Teams JavaScript.</span><span class="sxs-lookup"><span data-stu-id="295be-111">**Get experience with Teams tools and SDKs**: Customize your app with help from the Teams JavaScript client SDK.</span></span> <span data-ttu-id="295be-112">Например, измените цветовую схему приложения в соответствие с темой Teams.</span><span class="sxs-lookup"><span data-stu-id="295be-112">For example, change your app's color scheme to match the Teams theme.</span></span> <span data-ttu-id="295be-113">Кроме того, узнайте об общих средствах создания и управления ботами.</span><span class="sxs-lookup"><span data-stu-id="295be-113">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="295be-114">**Разойдитесь** по приложению. На протяжении уроков вы найдете связанные темы, которые вас, вероятно, интересуют (например, проверку подлинности и рекомендации по проектированию).</span><span class="sxs-lookup"><span data-stu-id="295be-114">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="295be-115">Основы приложений teams</span><span class="sxs-lookup"><span data-stu-id="295be-115">Teams app fundamentals</span></span>

<span data-ttu-id="295be-116">Прежде чем приступить к учебникам, необходимо знать следующее о создании приложений для Teams.</span><span class="sxs-lookup"><span data-stu-id="295be-116">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="295be-117">Приложения могут иметь несколько возможностей и точки входа</span><span class="sxs-lookup"><span data-stu-id="295be-117">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="295be-118">Приложение Teams состоит из одной или более возможностей [платформы](../concepts/capabilities-overview.md) (как люди используют приложение) и точек входа [(где](../concepts/extensibility-points.md) люди используют приложение).</span><span class="sxs-lookup"><span data-stu-id="295be-118">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) (how people use the app) and [entry points](../concepts/extensibility-points.md) (where people use the app).</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="295be-119">Teams не может принимать ваше приложение</span><span class="sxs-lookup"><span data-stu-id="295be-119">Teams doesn't host your app</span></span>

<span data-ttu-id="295be-120">Приложение Teams содержит следующие важные элементы:</span><span class="sxs-lookup"><span data-stu-id="295be-120">A Teams app includes the following important pieces:</span></span>

* <span data-ttu-id="295be-121">Логика, хранение данных и API вызывает, что питание приложения.</span><span class="sxs-lookup"><span data-stu-id="295be-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="295be-122">Эти службы не являются хостингом Teams и должны быть доступны с помощью HTTPS.</span><span class="sxs-lookup"><span data-stu-id="295be-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="295be-123">Клиент Teams (веб-, настольный или мобильный), в котором пользователи используют ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="295be-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="295be-124">ID приложения, который позволяет настраивать приложение с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="295be-124">Your app ID, which lets you configure your app with App Studio.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="295be-125">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="295be-125">Get prerequisites</span></span>

<span data-ttu-id="295be-126">Убедитесь, что у вас есть правая учетная запись для создания приложений Teams и установите некоторые рекомендуемые средства разработки.</span><span class="sxs-lookup"><span data-stu-id="295be-126">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="295be-127">Настройка учетной записи разработки</span><span class="sxs-lookup"><span data-stu-id="295be-127">Set up your development account</span></span>

<span data-ttu-id="295be-128">Вам нужна учетная запись Teams, которая позволяет настраивать загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="295be-128">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="295be-129">(Ваша учетная запись может уже предоставить это.)</span><span class="sxs-lookup"><span data-stu-id="295be-129">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="295be-130">Если у вас есть учетная запись Teams, убедитесь, что вы можете разгрузить приложения в Teams:</span><span class="sxs-lookup"><span data-stu-id="295be-130">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="295be-131">В клиенте Teams выберите **Приложения.**</span><span class="sxs-lookup"><span data-stu-id="295be-131">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="295be-132">Найди вариант **для загрузки настраиваемого приложения.**</span><span class="sxs-lookup"><span data-stu-id="295be-132">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, где в Teams можно загрузить настраиваемые приложения.":::
    
    <span data-ttu-id="295be-134">Если вы не видите кнопку, у вас нет разрешения на загрузку пользовательских приложений в вашей организации. Эту функцию можно получить, подписавшись на бесплатную подписку на разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="295be-134">If you don't see the button, you don't have permission to upload custom apps in your org. You can get this feature by signing up for a free Microsoft 365 developer subscription.</span></span>

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="295be-135"><b>Получите бесплатную подписку на разработчика Microsoft 365</b></span><span class="sxs-lookup"><span data-stu-id="295be-135"><b>Get your free Microsoft 365 developer subscription</b></span></span></summary>

<span data-ttu-id="295be-136">Вы можете получить бесплатную тестовую учетную запись Teams, которая позволяет загрузку приложений путем присоединения к программе разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="295be-136">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="295be-137">(Процесс регистрации занимает примерно две минуты.)</span><span class="sxs-lookup"><span data-stu-id="295be-137">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="295be-138">Перейдите к [программе разработчика Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="295be-138">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="295be-139">Выберите **Join Now** и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="295be-139">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="295be-140">Когда вы доберетсяе до экрана приветствия, выберите **настройка подписки E5**.</span><span class="sxs-lookup"><span data-stu-id="295be-140">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="295be-141">Настройка учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="295be-141">Set up your administrator account.</span></span> <span data-ttu-id="295be-142">Как только вы закончите, вы должны увидеть экран, как это.</span><span class="sxs-lookup"><span data-stu-id="295be-142">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации на программу разработчика Microsoft 365.":::
1. <span data-ttu-id="295be-144">Войдите в Teams с помощью только что настроенной учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="295be-144">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="295be-145">Убедитесь, что теперь у вас есть **настраиваемый параметр Upload приложения.**</span><span class="sxs-lookup"><span data-stu-id="295be-145">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

> [!Note]
> <span data-ttu-id="295be-146">Если вы все еще не можете загрузить приложения, см. в приложении включить настраиваемые [приложения Teams и включить настраиваемую загрузку приложений.](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)</span><span class="sxs-lookup"><span data-stu-id="295be-146">If you still can't sideload apps, see [enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

### <a name="install-your-development-tools"></a><span data-ttu-id="295be-147">Установка средств разработки</span><span class="sxs-lookup"><span data-stu-id="295be-147">Install your development tools</span></span>

<span data-ttu-id="295be-148">Приложения Teams можно создавать с помощью предпочтительных средств, но на этих уроках покажут, как быстро начать работу с microsoft Teams набор средств для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="295be-148">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="295be-149">Teams отображает содержимое приложения только с помощью подключений HTTPS.</span><span class="sxs-lookup"><span data-stu-id="295be-149">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="295be-150">Чтобы отламыть определенные типы приложений локально, например бот, вы узнаете, как использовать [ngrok](../concepts/build-and-test/debug.md#locally-hosted) для запуска безопасного туннеля между Teams и вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="295be-150">To debug certain types of apps locally, such as a bot, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="295be-151">(Приложения Production Teams находятся в облаке.)</span><span class="sxs-lookup"><span data-stu-id="295be-151">(Production Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="295be-152">Установите [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="295be-152">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="295be-153">Установите [ngrok,](https://ngrok.com/download) если вы строите бот или расширение обмена сообщениями и [создаете туннель с помощью ngrok.](https://docs.microsoft.com/microsoftteams/platform/tutorials/get-started-dotnet-app-studio#tunnel-using-ngrok)</span><span class="sxs-lookup"><span data-stu-id="295be-153">Install [ngrok](https://ngrok.com/download) if you are building a bot or messaging extension and [create a tunnel using ngrok](https://docs.microsoft.com/microsoftteams/platform/tutorials/get-started-dotnet-app-studio#tunnel-using-ngrok).</span></span>
1. <span data-ttu-id="295be-154">Установка последней версии [Visual Studio кода](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="295be-154">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="295be-155">(Более ранние версии могут не работать с набором инструментов.)</span><span class="sxs-lookup"><span data-stu-id="295be-155">(Earlier versions might not work with the toolkit.)</span></span>
1. В Visual Studio коде выберите **Расширения** на левой панели действий и установите :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: microsoft Teams **набор средств**.

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Иллюстрация, на которой Visual Studio коде можно установить расширение Microsoft Teams набор средств.":::

## <a name="about-the-tutorials"></a><span data-ttu-id="295be-158">Об учебных пособиях</span><span class="sxs-lookup"><span data-stu-id="295be-158">About the tutorials</span></span>

<span data-ttu-id="295be-159">Вы можете начать с любого из команд **начать** уроки.</span><span class="sxs-lookup"><span data-stu-id="295be-159">You can start with any of the Teams **get started** lessons.</span></span> <span data-ttu-id="295be-160">Если вы не знаете, куда перейти в первую очередь, следуйте нашим начинающим дружественным путем и создайте "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="295be-160">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="295be-161">приложение.</span><span class="sxs-lookup"><span data-stu-id="295be-161">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Дерево навыков с указанием путей обучения для уроков Teams 'get started'." border="false":::

## <a name="next-step"></a><span data-ttu-id="295be-163">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="295be-163">Next step</span></span>

<span data-ttu-id="295be-164">После создания учетной записи и среды можно приступить к построению.</span><span class="sxs-lookup"><span data-stu-id="295be-164">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="295be-165">Начинающий дружественный учебник</span><span class="sxs-lookup"><span data-stu-id="295be-165">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="295be-166">Создайте приложение "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="295be-166">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="295be-167">Другие учебники</span><span class="sxs-lookup"><span data-stu-id="295be-167">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="295be-168">Создание бота</span><span class="sxs-lookup"><span data-stu-id="295be-168">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="295be-169">Создание расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="295be-169">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
