---
title: Начало работы — создание первого обзорного приложения и предварительных условий
author: heath-hamilton
description: Узнайте, как начать разработку приложений Microsoft Teams и настроить среду.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: e2e73e755c45fa3bff3b6320dfbf0999a575fe99
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346814"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="430be-103">Общие сведения о создании первого приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="430be-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="430be-104">В разделе **Создание первых** приложений вы создадите базовые приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="430be-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="430be-105">В каждом учебном курсе описывается создание простого приложения Teams, а также общие инструменты, основные понятия и дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="430be-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="430be-106">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="430be-106">What you'll learn</span></span>

<span data-ttu-id="430be-107">Ниже представлены сведения о том, что вы узнаете после изучения уроков.</span><span class="sxs-lookup"><span data-stu-id="430be-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="430be-108">**Быстрый запуск и работа с набором инструментов Teams**: набор инструментов Microsoft Teams для Visual Studio Code создает проект приложения и формирование шаблонов, чтобы приложение могло работать в минутах.</span><span class="sxs-lookup"><span data-stu-id="430be-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="430be-109">**Настройте приложение с помощью App Studio**: Укажите возможности и службы, которые использует приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="430be-109">**Configure your app with App Studio**: Specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="430be-110">**Область аудиторий приложения**: создание приложения Teams для личного использования, совместной работы или и того, и другое.</span><span class="sxs-lookup"><span data-stu-id="430be-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
  > * <span data-ttu-id="430be-111">Узнайте, как использовать **средства Teams и пакеты SDK**: Настройка приложения (например, изменение цветовой схемы для согласования с темой Teams) с помощью справки из пакета SDK для Teams.</span><span class="sxs-lookup"><span data-stu-id="430be-111">**Get experience with Teams tools and SDKs**: Customize your app (for example, change its color scheme to match the Teams theme) with help from the Teams JavaScript SDK.</span></span> <span data-ttu-id="430be-112">Кроме того, Узнайте о стандартных средствах для создания и управления Боты.</span><span class="sxs-lookup"><span data-stu-id="430be-112">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="430be-113">**Разверните приложение на своем приложении**: в уроках вы найдете связанные темы (например, рекомендации по проверке подлинности и проектированию).</span><span class="sxs-lookup"><span data-stu-id="430be-113">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="430be-114">Основные сведения о приложениях Teams</span><span class="sxs-lookup"><span data-stu-id="430be-114">Teams app fundamentals</span></span>

<span data-ttu-id="430be-115">Прежде чем приступать к работе с руководствами, необходимо знать следующее о создании приложений для Teams.</span><span class="sxs-lookup"><span data-stu-id="430be-115">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="430be-116">Приложения могут иметь несколько возможностей и точек входа</span><span class="sxs-lookup"><span data-stu-id="430be-116">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="430be-117">Приложение Teams состоит из одной или нескольких [возможностей платформы](../concepts/capabilities-overview.md) (как люди используют приложение) и [точек входа](../concepts/extensibility-points.md) (где пользователи обнаруживают приложение).</span><span class="sxs-lookup"><span data-stu-id="430be-117">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) (how people use the app) and [entry points](../concepts/extensibility-points.md) (where people discover the app).</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="430be-118">В Teams не размещается ваше приложение</span><span class="sxs-lookup"><span data-stu-id="430be-118">Teams doesn't host your app</span></span>

<span data-ttu-id="430be-119">Приложение Teams включает следующие важные элементы:</span><span class="sxs-lookup"><span data-stu-id="430be-119">A Teams app includes the following important pieces:</span></span>

* <span data-ttu-id="430be-120">Логика, хранилище данных и вызовы API, которые переключают приложение.</span><span class="sxs-lookup"><span data-stu-id="430be-120">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="430be-121">Эти службы не размещаются в Teams и должны быть доступны по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="430be-121">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="430be-122">Клиент Teams (на веб-сайте, на настольном компьютере или мобильном устройстве), в котором пользователи используют ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="430be-122">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="430be-123">Идентификатор приложения, который позволяет настраивать приложение с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="430be-123">Your app ID, which lets you configure your app with App Studio.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="430be-124">Получение необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="430be-124">Get prerequisites</span></span>

<span data-ttu-id="430be-125">Убедитесь, что у вас есть правильная учетная запись для создания приложений Teams и установки некоторых рекомендуемых средств разработки.</span><span class="sxs-lookup"><span data-stu-id="430be-125">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="430be-126">Настройка учетной записи для разработки</span><span class="sxs-lookup"><span data-stu-id="430be-126">Set up your development account</span></span>

<span data-ttu-id="430be-127">Вам нужна учетная запись Teams, которая разрешает нестандартную загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="430be-127">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="430be-128">(Это может быть уже предоставлено вашей учетной записью.)</span><span class="sxs-lookup"><span data-stu-id="430be-128">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="430be-129">Если у вас есть учетная запись Teams, убедитесь, что вы можете Загрузка неопубликованных приложения в teams:</span><span class="sxs-lookup"><span data-stu-id="430be-129">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="430be-130">В клиенте Teams выберите **приложения**.</span><span class="sxs-lookup"><span data-stu-id="430be-130">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="430be-131">Найдите параметр для **отправки настраиваемого приложения**.</span><span class="sxs-lookup"><span data-stu-id="430be-131">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Иллюстрация, на которой показано, где в Teams вы можете отправить пользовательское приложение.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="430be-133">Если вы не видите параметр Загрузка неопубликованных или у вас нет учетной записи Teams, <b>выберите здесь</b> .</span><span class="sxs-lookup"><span data-stu-id="430be-133"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="430be-134">Вы можете получить бесплатную тестовую учетную запись Teams, позволяющую выполнять загрузку неопубликованных приложений, присоединяясь к программе для разработчиков Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="430be-134">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="430be-135">(Процесс регистрации занимает около двух минут.)</span><span class="sxs-lookup"><span data-stu-id="430be-135">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="430be-136">Перейдите к [программе для разработчиков Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="430be-136">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="430be-137">Нажмите кнопку **присоединиться сейчас** и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="430be-137">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="430be-138">При получении экрана приветствия выберите пункт **настроить подписку** по клавише вверх.</span><span class="sxs-lookup"><span data-stu-id="430be-138">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="430be-139">Настройте учетную запись администратора.</span><span class="sxs-lookup"><span data-stu-id="430be-139">Set up your administrator account.</span></span> <span data-ttu-id="430be-140">После завершения вы увидите экран следующего вида:</span><span class="sxs-lookup"><span data-stu-id="430be-140">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации в программе для разработчиков Microsoft 365.":::
1. <span data-ttu-id="430be-142">Войдите в Teams с помощью учетной записи администратора, которую вы только что настроили.</span><span class="sxs-lookup"><span data-stu-id="430be-142">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="430be-143">Убедитесь, что у вас теперь есть параметр **Отправить настраиваемое приложение** .</span><span class="sxs-lookup"><span data-stu-id="430be-143">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

> [!Note]
> <span data-ttu-id="430be-144">Если вы по-прежнему не можете Загрузка неопубликованных приложения, обратитесь к разделу [Включение пользовательских приложений Teams и включите пользовательскую отправку приложений](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span><span class="sxs-lookup"><span data-stu-id="430be-144">If you still can't sideload apps, refer to [Enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

### <a name="install-your-development-tools"></a><span data-ttu-id="430be-145">Установка средств разработки</span><span class="sxs-lookup"><span data-stu-id="430be-145">Install your development tools</span></span>

<span data-ttu-id="430be-146">Вы можете создавать приложения Teams с помощью своих предпочтительных средств, но на этих занятиях показано, как быстро начать работу с набором инструментов Microsoft Teams для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="430be-146">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="430be-147">Teams отображает контент приложения только через HTTPS подключения.</span><span class="sxs-lookup"><span data-stu-id="430be-147">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="430be-148">Для отладки определенных типов приложений, таких как Bot, вы узнаете, как использовать [ngrok для настройки безопасного туннеля](../concepts/build-and-test/debug.md#locally-hosted) между Teams и приложением.</span><span class="sxs-lookup"><span data-stu-id="430be-148">To debug certain types of apps locally, such as a bot, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="430be-149">(Рабочие группы приложений размещаются в облаке.)</span><span class="sxs-lookup"><span data-stu-id="430be-149">(Production Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="430be-150">Установите [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="430be-150">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="430be-151">Установите [ngrok](https://ngrok.com/download) , если вы собираетесь создать расширение Bot или Messaging.</span><span class="sxs-lookup"><span data-stu-id="430be-151">Install [ngrok](https://ngrok.com/download) if you plan to build a bot or messaging extension.</span></span>
1. <span data-ttu-id="430be-152">Установите последнюю версию [Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="430be-152">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="430be-153">(Более ранние версии могут не работать с этим набором инструментов.)</span><span class="sxs-lookup"><span data-stu-id="430be-153">(Earlier versions might not work with the toolkit.)</span></span>
1. В Visual Studio Code выберите **расширения** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: на левой панели действий и установите **набор инструментов Microsoft Teams**.

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Иллюстрация, в которой показано, где в Visual Studio Code Вы можете установить расширение набора инструментов Microsoft Teams.":::

## <a name="about-the-tutorials"></a><span data-ttu-id="430be-156">Сведения о учебниках</span><span class="sxs-lookup"><span data-stu-id="430be-156">About the tutorials</span></span>

<span data-ttu-id="430be-157">Вы можете начать с любой из Teams, чтобы **создать первые уроки приложений** .</span><span class="sxs-lookup"><span data-stu-id="430be-157">You can start with any of the Teams **build your first app** lessons.</span></span> <span data-ttu-id="430be-158">Если вы не знаете, где сначала перейти, сделайте наш дружественный путь и создайте "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="430be-158">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="430be-159">программы.</span><span class="sxs-lookup"><span data-stu-id="430be-159">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Дерево навыков, в котором показаны пути обучения для Teams для работы с учебными руководствами по созданию первого приложения." border="false":::

## <a name="next-step"></a><span data-ttu-id="430be-161">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="430be-161">Next step</span></span>

<span data-ttu-id="430be-162">После настройки учетной записи и среды можно приступить к созданию.</span><span class="sxs-lookup"><span data-stu-id="430be-162">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="430be-163">Удобное руководство для начинающих</span><span class="sxs-lookup"><span data-stu-id="430be-163">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="430be-164">Создание приложения "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="430be-164">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="430be-165">Другие учебные пособия</span><span class="sxs-lookup"><span data-stu-id="430be-165">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="430be-166">Создание бота</span><span class="sxs-lookup"><span data-stu-id="430be-166">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="430be-167">Создание расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="430be-167">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
