---
title: Начало работы — создание первого обзора приложения и необходимых условий
author: heath-hamilton
description: Узнайте, как начать разработку приложений Microsoft Teams и настроить среду.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 4288efdbfada5f1a51fa1d4aeccdd6cdf9c64382
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797899"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="7d399-103">Создание первого обзора приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7d399-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="7d399-104">На **уроках по началу** работы вы узнаете, как создавать базовые приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="7d399-104">In the **get started** lessons, you learn how to create basic Teams apps.</span></span> <span data-ttu-id="7d399-105">В каждом руководстве поется о том, как создать простое, реальное приложение Teams, а также общие инструменты, основные понятия и более сложные функции.</span><span class="sxs-lookup"><span data-stu-id="7d399-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="7d399-106">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="7d399-106">What you'll learn</span></span>

<span data-ttu-id="7d399-107">Вот представление о том, что вы узнаете после уроков.</span><span class="sxs-lookup"><span data-stu-id="7d399-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="7d399-108">Быстрое создание и запуск teams **набор средств:** Microsoft Teams набор средств for Visual Studio Code создает проект приложения и создает скафолдинг, чтобы у вас было запущено приложение за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7d399-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="7d399-109">**Настройте приложение с помощью App Studio:** укажите возможности и службы, которые использует ваше приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="7d399-109">**Configure your app with App Studio**: Specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="7d399-110">**Область аудитории приложения:** создайте приложение Teams для личного использования, совместной работы или и того, и другое.</span><span class="sxs-lookup"><span data-stu-id="7d399-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
> * <span data-ttu-id="7d399-111">Получите опыт работы со средствами Teams и **SDK:** настройте приложение с помощью клиентского SDK JavaScript для Teams.</span><span class="sxs-lookup"><span data-stu-id="7d399-111">**Get experience with Teams tools and SDKs**: Customize your app with help from the Teams JavaScript client SDK.</span></span> <span data-ttu-id="7d399-112">Например, измените цветовую схему приложения в соответствие с темой Teams.</span><span class="sxs-lookup"><span data-stu-id="7d399-112">For example, change your app's color scheme to match the Teams theme.</span></span> <span data-ttu-id="7d399-113">Кроме того, узнайте о распространенных средствах для создания ботов и управления их.</span><span class="sxs-lookup"><span data-stu-id="7d399-113">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="7d399-114">**Разберите свое** приложение. Во время уроков вы найдете интересуя вас связанные темы (например, руководство по проверке подлинности и проектированию).</span><span class="sxs-lookup"><span data-stu-id="7d399-114">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="7d399-115">Основы приложения Teams</span><span class="sxs-lookup"><span data-stu-id="7d399-115">Teams app fundamentals</span></span>

<span data-ttu-id="7d399-116">Прежде чем приступить к учебникам, необходимо знать следующее о создании приложений для Teams.</span><span class="sxs-lookup"><span data-stu-id="7d399-116">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="7d399-117">Приложения могут иметь несколько возможностей и точек входа</span><span class="sxs-lookup"><span data-stu-id="7d399-117">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="7d399-118">Приложение Teams состоит из одной или более возможностей [платформы](../concepts/capabilities-overview.md) (как люди используют приложение) и точек входа [(где](../concepts/extensibility-points.md) люди используют приложение).</span><span class="sxs-lookup"><span data-stu-id="7d399-118">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) (how people use the app) and [entry points](../concepts/extensibility-points.md) (where people use the app).</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="7d399-119">Приложение не в Teams</span><span class="sxs-lookup"><span data-stu-id="7d399-119">Teams doesn't host your app</span></span>

<span data-ttu-id="7d399-120">Приложение Teams включает следующие важные элементы:</span><span class="sxs-lookup"><span data-stu-id="7d399-120">A Teams app includes the following important pieces:</span></span>

* <span data-ttu-id="7d399-121">Логика, хранилище данных и API-вызовы, которые могут быть в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="7d399-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="7d399-122">Эти службы не находятся в Teams и должны быть доступны по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7d399-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="7d399-123">Клиент Teams (веб-, настольный или мобильный), в котором пользователи используют ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="7d399-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="7d399-124">ИД приложения, который позволяет настроить приложение с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="7d399-124">Your app ID, which lets you configure your app with App Studio.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="7d399-125">Получить необходимые условия</span><span class="sxs-lookup"><span data-stu-id="7d399-125">Get prerequisites</span></span>

<span data-ttu-id="7d399-126">Убедитесь, что у вас есть учетная запись для создания приложений Teams и установите некоторые рекомендуемые средства разработки.</span><span class="sxs-lookup"><span data-stu-id="7d399-126">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="7d399-127">Настройка учетной записи разработки</span><span class="sxs-lookup"><span data-stu-id="7d399-127">Set up your development account</span></span>

<span data-ttu-id="7d399-128">Вам нужна учетная запись Teams, которая позволяет настраивать загрузку нео том же приложения.</span><span class="sxs-lookup"><span data-stu-id="7d399-128">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="7d399-129">(Возможно, ваша учетная запись уже предоставила это.)</span><span class="sxs-lookup"><span data-stu-id="7d399-129">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="7d399-130">Если у вас есть учетная запись Teams, проверьте, можете ли вы загрузку неогрузки приложений в Teams:</span><span class="sxs-lookup"><span data-stu-id="7d399-130">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="7d399-131">В клиенте Teams выберите **"Приложения".**</span><span class="sxs-lookup"><span data-stu-id="7d399-131">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="7d399-132">Найди вариант **отправки настраиваемого приложения.**</span><span class="sxs-lookup"><span data-stu-id="7d399-132">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, где в Teams можно отправить пользовательское приложение.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="7d399-134"><b>Выберите здесь,</b> если не видите параметр загрузки неогрузки или у вас нет учетной записи Teams.</span><span class="sxs-lookup"><span data-stu-id="7d399-134"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="7d399-135">Вы можете получить бесплатную тестовую учетную запись Teams, которая позволяет загрузку неогрузки приложения, присоединившись к программе для разработчиков Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="7d399-135">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="7d399-136">(Процесс регистрации занимает приблизительно две минуты.)</span><span class="sxs-lookup"><span data-stu-id="7d399-136">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="7d399-137">Перейдите в [программу для разработчиков Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="7d399-137">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="7d399-138">Выберите **"Присоединиться сейчас"** и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="7d399-138">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="7d399-139">When you get to the welcome screen, select **Set up E5 subscription**.</span><span class="sxs-lookup"><span data-stu-id="7d399-139">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="7d399-140">Настройка учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="7d399-140">Set up your administrator account.</span></span> <span data-ttu-id="7d399-141">После завершения вы увидите экран, похожий на этот.</span><span class="sxs-lookup"><span data-stu-id="7d399-141">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации в программе для разработчиков Microsoft 365.":::
1. <span data-ttu-id="7d399-143">Войдите в Teams с помощью только что настроенной учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="7d399-143">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="7d399-144">Проверьте, есть ли у вас параметр **отправки настраиваемого** приложения.</span><span class="sxs-lookup"><span data-stu-id="7d399-144">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

> [!Note]
> <span data-ttu-id="7d399-145">Если вы по-прежнему не можете загружать неогружаемые приложения, включите настраиваемые приложения Teams и включите отправку [пользовательских приложений.](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)</span><span class="sxs-lookup"><span data-stu-id="7d399-145">If you still can't sideload apps, see [enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

### <a name="install-your-development-tools"></a><span data-ttu-id="7d399-146">Установка средств разработки</span><span class="sxs-lookup"><span data-stu-id="7d399-146">Install your development tools</span></span>

<span data-ttu-id="7d399-147">Вы можете создавать приложения Teams с помощью предпочитаемых инструментов, но эти уроки показывают, как быстро начать работу с microsoft Teams набор средств для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7d399-147">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="7d399-148">Teams отображает содержимое приложения только через ПОДКЛЮЧЕНИЯ HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7d399-148">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="7d399-149">Для локальной отлаки определенных типов приложений, таких как бот, вы узнаете, как использовать [ngrok](../concepts/build-and-test/debug.md#locally-hosted) для настроить безопасный туннель между Teams и вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="7d399-149">To debug certain types of apps locally, such as a bot, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="7d399-150">(Приложения Production Teams находятся в облаке.)</span><span class="sxs-lookup"><span data-stu-id="7d399-150">(Production Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="7d399-151">Установите [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="7d399-151">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="7d399-152">Установите [ngrok,](https://ngrok.com/download) если вы планируете создать бота или расширение для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="7d399-152">Install [ngrok](https://ngrok.com/download) if you plan to build a bot or messaging extension.</span></span>
1. <span data-ttu-id="7d399-153">Установите последнюю версию [Visual Studio Code.](https://code.visualstudio.com/download)</span><span class="sxs-lookup"><span data-stu-id="7d399-153">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="7d399-154">(Более ранние версии могут не работать с набором средств.)</span><span class="sxs-lookup"><span data-stu-id="7d399-154">(Earlier versions might not work with the toolkit.)</span></span>
1. В Visual Studio code выберите **"Расширения"** в левой панели действий и установите :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: microsoft Teams **набор средств.**

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Иллюстрация, на которой по Visual Studio Code можно установить расширение Microsoft Teams набор средств.":::

## <a name="about-the-tutorials"></a><span data-ttu-id="7d399-157">Об учебниках</span><span class="sxs-lookup"><span data-stu-id="7d399-157">About the tutorials</span></span>

<span data-ttu-id="7d399-158">Вы можете начать с любого из уроков по **началу** работы с Teams.</span><span class="sxs-lookup"><span data-stu-id="7d399-158">You can start with any of the Teams **get started** lessons.</span></span> <span data-ttu-id="7d399-159">Если вы не знаете, куда перейти в первую очередь, следуйте нашему начинающему удобному пути и создайте "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="7d399-159">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="7d399-160">app.</span><span class="sxs-lookup"><span data-stu-id="7d399-160">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Дерево навыков, в котором показаны учебные пути для уроков &quot;начало работы&quot; Teams." border="false":::

## <a name="next-step"></a><span data-ttu-id="7d399-162">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="7d399-162">Next step</span></span>

<span data-ttu-id="7d399-163">После того как вы настроите свою учетную запись и среду, вы сможете приступить к построению.</span><span class="sxs-lookup"><span data-stu-id="7d399-163">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="7d399-164">Обучающие курсы для начинающих</span><span class="sxs-lookup"><span data-stu-id="7d399-164">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d399-165">Создание приложения "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="7d399-165">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="7d399-166">Другие учебники</span><span class="sxs-lookup"><span data-stu-id="7d399-166">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d399-167">Создание бота</span><span class="sxs-lookup"><span data-stu-id="7d399-167">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="7d399-168">Создание расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="7d399-168">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
