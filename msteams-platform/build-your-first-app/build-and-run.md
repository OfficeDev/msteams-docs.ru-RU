---
title: Начало работы — сборка и запуск первого приложения
author: girliemac
description: Быстро создайте приложение Microsoft Teams, которое отображает "Hello, World!" сообщение с помощью microsoft Teams набор средств.
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: b34409919f073535c741a48edf30f3edd8c6bc8f
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068803"
---
# <a name="create-your-first-microsoft-teams-app"></a><span data-ttu-id="533b4-104">Создание первого приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="533b4-104">Create your first Microsoft Teams app</span></span>

<span data-ttu-id="533b4-105">Этот quickstart учит вас создавать и запускать приложение Microsoft Teams, которое отображает "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="533b4-105">This quickstart teaches you to build and run Microsoft Teams app that displays "Hello, World!"</span></span>

## <a name="prerequisites"></a><span data-ttu-id="533b4-106">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="533b4-106">Prerequisites</span></span>

<span data-ttu-id="533b4-107">Перед началом работы необходимо настроить клиента разработки [Teams](#set-up-your-teams-development-tenant) и [установить средства разработки Teams.](#install-your-development-tools)</span><span class="sxs-lookup"><span data-stu-id="533b4-107">Before you begin, you need to [set up your Teams development tenant](#set-up-your-teams-development-tenant) and [install your Teams development tools](#install-your-development-tools).</span></span>

### <a name="set-up-your-teams-development-tenant"></a><span data-ttu-id="533b4-108">Настройка клиента разработки Teams</span><span class="sxs-lookup"><span data-stu-id="533b4-108">Set up your Teams development tenant</span></span>

<span data-ttu-id="533b4-109">Клиент **—** это как контейнер для организации.</span><span class="sxs-lookup"><span data-stu-id="533b4-109">A **tenant** is like a container for an organization.</span></span> <span data-ttu-id="533b4-110">В терминах Teams клиент — это место, где люди из этого орга-чата делятся файлами и запускают собрания.</span><span class="sxs-lookup"><span data-stu-id="533b4-110">In Teams terms, a tenant is where people from that org chat, share files, and run meetings.</span></span> <span data-ttu-id="533b4-111">В качестве разработчика необходимо, чтобы клиент перегружал и тестировали строимые приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="533b4-111">As a developer, you need a tenant to sideload and test the Teams apps that you are building.</span></span>  

# <a name="do-not-have-a-tenant"></a>[<span data-ttu-id="533b4-112">Нет клиента</span><span class="sxs-lookup"><span data-stu-id="533b4-112">Do not have a tenant</span></span>](#tab/do-not-have-a-tenant)

<span data-ttu-id="533b4-113">Вы можете получить бесплатную тестовую учетную запись Teams, которая включает клиента, который позволяет загрузку приложений, присоединившись к программе разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="533b4-113">You can get a free Teams test account, which includes a tenant that allows app sideloading, by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="533b4-114">Процесс регистрации занимает примерно две минуты.</span><span class="sxs-lookup"><span data-stu-id="533b4-114">The registration process takes approximately two minutes.</span></span>

<span data-ttu-id="533b4-115">**Чтобы получить клиента**</span><span class="sxs-lookup"><span data-stu-id="533b4-115">**To get a tenant**</span></span>

1. <span data-ttu-id="533b4-116">Перейдите к [программе разработчика Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="533b4-116">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="533b4-117">Выберите **Join Now** и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="533b4-117">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="533b4-118">На экране Welcome выберите **настройка подписки E5.**</span><span class="sxs-lookup"><span data-stu-id="533b4-118">In the Welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="533b4-119">Настройка учетной записи разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="533b4-119">Set up your Microsoft 365 developer account.</span></span> 
   <span data-ttu-id="533b4-120">После завершения отображается следующий экран:</span><span class="sxs-lookup"><span data-stu-id="533b4-120">After you finish, the following screen appears:</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации на программу разработчика Microsoft 365.":::

1. <span data-ttu-id="533b4-122">Во входе в Teams с новой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="533b4-122">Sign in to Teams with your new account.</span></span>
1. <span data-ttu-id="533b4-123">В клиенте Teams выберите **Приложения.**</span><span class="sxs-lookup"><span data-stu-id="533b4-123">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="533b4-124">Убедитесь, что вы можете увидеть **параметр Upload настраиваемого** приложения.</span><span class="sxs-lookup"><span data-stu-id="533b4-124">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="533b4-125">Если вы это сделаете, это означает, что вы можете перегружать приложения.</span><span class="sxs-lookup"><span data-stu-id="533b4-125">If you do, this means you can sideload apps.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, где в Teams можно загрузить настраиваемые приложения.":::

# <a name="have-a-tenant"></a>[<span data-ttu-id="533b4-127">Иметь клиента</span><span class="sxs-lookup"><span data-stu-id="533b4-127">Have a tenant</span></span>](#tab/have-a-tenant)

<span data-ttu-id="533b4-128">Если у вас уже есть клиент, проверьте, можно ли перегружать приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="533b4-128">If you already have a tenant, verify if you can sideload apps in Teams.</span></span>

<span data-ttu-id="533b4-129">**Убедитесь, что приложения можно перегружать в сторону**</span><span class="sxs-lookup"><span data-stu-id="533b4-129">**Verify that you can sideload your apps**</span></span> 

1. <span data-ttu-id="533b4-130">В клиенте Teams выберите **Приложения.**</span><span class="sxs-lookup"><span data-stu-id="533b4-130">In the Teams Client, select **Apps**.</span></span> 
1.  <span data-ttu-id="533b4-131">Убедитесь, что вы можете увидеть **параметр Upload настраиваемого** приложения.</span><span class="sxs-lookup"><span data-stu-id="533b4-131">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="533b4-132">Если вы это сделаете, это означает, что вы можете перегружать приложения.</span><span class="sxs-lookup"><span data-stu-id="533b4-132">If you do, this means you can sideload apps.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, где в Teams можно загрузить настраиваемые приложения.":::

---

### <a name="install-your-development-tools"></a><span data-ttu-id="533b4-134">Установка средств разработки</span><span class="sxs-lookup"><span data-stu-id="533b4-134">Install your development tools</span></span>

<span data-ttu-id="533b4-135">Чтобы создать это приложение, для быстрого начала работы набор средств teams Visual Studio код.</span><span class="sxs-lookup"><span data-stu-id="533b4-135">To build this app, you'll use the Teams Toolkit for Visual Studio Code to quickly get started.</span></span> <span data-ttu-id="533b4-136">Вы также можете создавать приложения Teams с любыми из заранее.</span><span class="sxs-lookup"><span data-stu-id="533b4-136">You can also build Teams apps with any ofyour preffered tools.</span></span> 

> [!NOTE]
> <span data-ttu-id="533b4-137">Teams отображает содержимое приложения только с помощью подключений HTTPS.</span><span class="sxs-lookup"><span data-stu-id="533b4-137">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="533b4-138">Чтобы отламыть определенные типы приложений локально, например бот, вы узнаете, как использовать ngrok для запуска безопасного туннеля между Teams и вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="533b4-138">To debug certain types of apps locally, such as a bot, you'll learn how to use ngrok to set up a secure tunnel between Teams and your app.</span></span>
> 
> <span data-ttu-id="533b4-139">Приложения Production Teams находятся в облаке.</span><span class="sxs-lookup"><span data-stu-id="533b4-139">Production Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="533b4-140">**Установка средств Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="533b4-140">**To install Microsoft Teams tools**</span></span>

1. <span data-ttu-id="533b4-141">Установите [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="533b4-141">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="533b4-142">Если вы планируете создать расширение бота или обмена сообщениями, установите [ngrok](https://ngrok.com/download) и выставите локальный интернет с помощью [ngrok.](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok)</span><span class="sxs-lookup"><span data-stu-id="533b4-142">If you plan to build a bot or messaging extension, install [ngrok](https://ngrok.com/download) and [expose your localhost to the Internet using ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok).</span></span>
1. <span data-ttu-id="533b4-143">Установка последней версии [Visual Studio кода](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="533b4-143">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="533b4-144">Набор инструментов не поддерживает более ранние версии Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="533b4-144">The toolkit does not support earlier versions of Visual Studio Code.</span></span>

1. В левой панели действий выберите **Расширения.** :::image type="icon" source="../assets/icons/vs-code-extensions.png":::
1. <span data-ttu-id="533b4-146">В **Microsoft Teams набор средств** установите **.**</span><span class="sxs-lookup"><span data-stu-id="533b4-146">In **Microsoft Teams Toolkit**, select **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Иллюстрация, на которой Visual Studio коде можно установить расширение Microsoft Teams набор средств.":::

## <a name="1-create-your-app-project"></a><span data-ttu-id="533b4-148">1. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="533b4-148">1. Create your app project</span></span>

1. <span data-ttu-id="533b4-149">Откройте Visual Studio код.</span><span class="sxs-lookup"><span data-stu-id="533b4-149">Open Visual Studio Code.</span></span>
1. Выберите **Microsoft Teams набор средств** создать новое приложение :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **Teams.**

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="Снимок экрана, показывающий, как создать проект приложения с помощью Visual Studio команд кода набор средств.":::
   
1. <span data-ttu-id="533b4-152">Во входе с учетной записью разработки Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="533b4-152">Sign in with your Microsoft 365 development account.</span></span> <span data-ttu-id="533b4-153">Либо только что созданная учетная запись, либо уже созданная учетная запись, которая позволяет загрузку приложения в сторону.</span><span class="sxs-lookup"><span data-stu-id="533b4-153">Either the one you just created or the account you already had that allows app sideloading.</span></span>
1. <span data-ttu-id="533b4-154">На экране **Выберите проект** перейдите в приложение **Personal и** выберите **JS** (JavaScript) > **Далее**.</span><span class="sxs-lookup"><span data-stu-id="533b4-154">On the **Select project** screen, go to **Personal app** and select **JS** (JavaScript) > **Next**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Снимок экрана, показывающий, как настроить проект приложения с помощью Visual Studio команд кода набор средств.":::

1. <span data-ttu-id="533b4-156">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="533b4-156">Enter a name for your Teams app.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="Снимок экрана, показывающий, как добавить имя в проект приложения с помощью Visual Studio code Teams набор средств.":::

1. <span data-ttu-id="533b4-158">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="533b4-158">Select **Finish**.</span></span> 
   <span data-ttu-id="533b4-159">Теперь проект настроен.</span><span class="sxs-lookup"><span data-stu-id="533b4-159">Your project is now configured.</span></span> 

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="533b4-160">2. Понимание компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="533b4-160">2. Understand your app project components</span></span>

<span data-ttu-id="533b4-161">После того как набор инструментов настроит проект приложения, у вас будут компоненты для создания "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="533b4-161">After the toolkit configures your app project, you have the components to build your "Hello, World!"</span></span> <span data-ttu-id="533b4-162">Приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="533b4-162">Teams app.</span></span> <span data-ttu-id="533b4-163">Каталоги и файлы проекта находятся в Visual Studio Code Explorer.</span><span class="sxs-lookup"><span data-stu-id="533b4-163">The project's directories and files are located in the Visual Studio Code Explorer.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="Снимок экрана, показывающий леса в проекте приложения с Visual Studio code Teams набор средств.":::

<span data-ttu-id="533b4-165">Набор инструментов автоматически создает строительные леса приложений в каталоге на основе возможностей, добавленных `src` во время установки.</span><span class="sxs-lookup"><span data-stu-id="533b4-165">The toolkit automatically creates app scaffolding in the `src` directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="533b4-166">Так как вы создали вкладку во время настройки, файл в каталоге обрабатывает инициализацию и `App.js` `src/components` маршрутизацию приложения.</span><span class="sxs-lookup"><span data-stu-id="533b4-166">Since you created a tab during setup, the `App.js` file in the `src/components` directory handles the initialization and routing of your app.</span></span> <span data-ttu-id="533b4-167">Файл также вызывает SDK клиента Microsoft Teams JavaScript для установления связи между вашим приложением и teams.</span><span class="sxs-lookup"><span data-stu-id="533b4-167">The file also calls the Microsoft Teams JavaScript client SDK to establish communication between your app and Teams.</span></span> 

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="533b4-168">3. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="533b4-168">3. Build and run your app</span></span>

<span data-ttu-id="533b4-169">Создайте и запустите приложение локально, чтобы сэкономить время.</span><span class="sxs-lookup"><span data-stu-id="533b4-169">Build and run your app locally to save time.</span></span> 

<span data-ttu-id="533b4-170">**Создание и запуск приложения**</span><span class="sxs-lookup"><span data-stu-id="533b4-170">**To build and run your app**</span></span>

1. <span data-ttu-id="533b4-171">В Visual Studio коде выберите **Терминал**  >  **Представления**.</span><span class="sxs-lookup"><span data-stu-id="533b4-171">In Visual Studio Code, select **View** > **Terminal**.</span></span>
1. <span data-ttu-id="533b4-172">Запуск `npm install` .</span><span class="sxs-lookup"><span data-stu-id="533b4-172">Run `npm install`.</span></span>
1. <span data-ttu-id="533b4-173">Запуск `npm start` .</span><span class="sxs-lookup"><span data-stu-id="533b4-173">Run `npm start`.</span></span>
  
  <span data-ttu-id="533b4-174">**Компилировать успешно!**</span><span class="sxs-lookup"><span data-stu-id="533b4-174">A **Compiled successfully!**</span></span> <span data-ttu-id="533b4-175">сообщение отображается в терминале.</span><span class="sxs-lookup"><span data-stu-id="533b4-175">message appears in the terminal.</span></span> <span data-ttu-id="533b4-176">Ваше приложение теперь работает на локальном сайте по `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="533b4-176">Your app is now running on your localhost at `https://localhost:3000`.</span></span> 

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="533b4-177">4. Sideload ваше приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="533b4-177">4. Sideload your app in Teams</span></span>

<span data-ttu-id="533b4-178">Sideloading — это процесс установки приложения в Teams, которое не было утверждено вашим администратором или Корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="533b4-178">Sideloading is the process of installing an app in Teams that hasn't been approved by your admin or Microsoft.</span></span> <span data-ttu-id="533b4-179">При тестировании и отладке приложений Teams часто используется боковая загрузка.</span><span class="sxs-lookup"><span data-stu-id="533b4-179">Sideloading is common when testing and debugging Teams apps.</span></span>

<span data-ttu-id="533b4-180">По умолчанию Teams не разрешает загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="533b4-180">By default, Teams doesn't allow app sideloading.</span></span> <span data-ttu-id="533b4-181">Этот параметр можно изменить в центре администрирования Teams.</span><span class="sxs-lookup"><span data-stu-id="533b4-181">You can change this setting in the Teams admin center.</span></span>

<span data-ttu-id="533b4-182">**Чтобы включить загрузку приложений в Teams**</span><span class="sxs-lookup"><span data-stu-id="533b4-182">**To enable app sideloading in Teams**</span></span>

1. <span data-ttu-id="533b4-183">Во входе в [центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="533b4-183">Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>  
1. <span data-ttu-id="533b4-184">Выберите **Показать все**  >  **команды.**</span><span class="sxs-lookup"><span data-stu-id="533b4-184">Select **Show All** > **Teams**.</span></span> 

   ![изображение меню центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > <span data-ttu-id="533b4-186">Для появления параметра **Teams** может занять до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="533b4-186">It can take up to 24 hours for the **Teams** option to appear.</span></span> 

1. <span data-ttu-id="533b4-187">Перейдите к **политикам установки приложений Teams**  >    >  **Global** (по умолчанию в масштабах всей организации).</span><span class="sxs-lookup"><span data-stu-id="533b4-187">Go to **Teams apps** > **Setup policies** > **Global** (Org-wide default).</span></span>

   ![включить представление боковой нагрузки](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. <span data-ttu-id="533b4-189">Включите **переключить настраиваемые приложения** для загрузки.</span><span class="sxs-lookup"><span data-stu-id="533b4-189">Turn on the **upload custom apps** toggle.</span></span>

1. <span data-ttu-id="533b4-190">Выберите **Сохранить,** чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="533b4-190">Select **Save** to save the changes.</span></span>

   <span data-ttu-id="533b4-191">Клиент тестового клиента теперь разрешает настраиваемую загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="533b4-191">Your test tenant now allows custom app sideloading.</span></span>

   > [!Note]
   > <span data-ttu-id="533b4-192">Проверьте проблемы перед загрузкой приложения с помощью функции проверки в App Studio, которая входит в набор инструментов.</span><span class="sxs-lookup"><span data-stu-id="533b4-192">Check for issues before sideloading your app using the validation feature in App Studio, which is included in the toolkit.</span></span> <span data-ttu-id="533b4-193">Устранение ошибок для успешной загрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="533b4-193">Fix the errors to successfully sideload the app.</span></span>


### <a name="sideload-your-app"></a><span data-ttu-id="533b4-194">Боковая загрузка приложения</span><span class="sxs-lookup"><span data-stu-id="533b4-194">Sideload your app</span></span>

1. <span data-ttu-id="533b4-195">В Visual Studio коде откройте командную набор средств.</span><span class="sxs-lookup"><span data-stu-id="533b4-195">In Visual Studio Code, open the Teams Toolkit.</span></span>
1. <span data-ttu-id="533b4-196">Перейдите в **App Studio**.</span><span class="sxs-lookup"><span data-stu-id="533b4-196">Go to **App Studio**.</span></span>  
1. <span data-ttu-id="533b4-197">Выберите **тест и раздайте**  >  **установку.**</span><span class="sxs-lookup"><span data-stu-id="533b4-197">Select **Test and Distribute** > **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="Снимок экрана, показывающий, как перегрузить приложение в клиент Teams с помощью Visual Studio команд кода набор средств.":::

<span data-ttu-id="533b4-199">**В качестве альтернативы**</span><span class="sxs-lookup"><span data-stu-id="533b4-199">**Alternatively**</span></span>

1. <span data-ttu-id="533b4-200">Выберите **клавишу F5,** чтобы открыть окно браузера для установки.</span><span class="sxs-lookup"><span data-stu-id="533b4-200">Select the **F5** key to open browser window to install.</span></span> <span data-ttu-id="533b4-201">Это позволит пропустить процесс установки в **App Studio** и lauch Teams в браузере.</span><span class="sxs-lookup"><span data-stu-id="533b4-201">This will skip the installation process in the **App Studio** and lauch Teams in your browser.</span></span>
1. <span data-ttu-id="533b4-202">В диалоговом окте установки выберите **Добавить** для установки приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="533b4-202">In the installation dialog, select **Add** to install your app to Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="Снимок экрана, показывающий, как перегрузить приложение в клиент Teams.":::

   > [!Note]
   > <span data-ttu-id="533b4-204">App Studio также доступен в качестве отдельного приложения для клиента Teams.</span><span class="sxs-lookup"><span data-stu-id="533b4-204">App Studio is also available as a stand-alone app for Teams client.</span></span>

### <a name="troubleshoot-sideloading-issues"></a><span data-ttu-id="533b4-205">Устранение неполадок при перегрузке</span><span class="sxs-lookup"><span data-stu-id="533b4-205">Troubleshoot sideloading issues</span></span>

<span data-ttu-id="533b4-206">**Сбой установки**</span><span class="sxs-lookup"><span data-stu-id="533b4-206">**Installation failed**</span></span>

<span data-ttu-id="533b4-207">Если сообщение об ошибке появляется при установке приложения, убедитесь, что сведения о приложении правильно `Manifest parsing has failed` введены.</span><span class="sxs-lookup"><span data-stu-id="533b4-207">If the `Manifest parsing has failed` error message appears while installing your app, verify that the app information is correctly entered.</span></span>

<span data-ttu-id="533b4-208">**Проверка сведений о приложении**</span><span class="sxs-lookup"><span data-stu-id="533b4-208">**To verify the app information**</span></span>

* <span data-ttu-id="533b4-209">В командной набор средств перейдите в **App Studio** App и убедитесь, что вся необходимая информация введена  >   правильно.</span><span class="sxs-lookup"><span data-stu-id="533b4-209">In the Teams Toolkit, go to **App Studio** > **App details** and verify that all the required information is correctly entered.</span></span>
*  <span data-ttu-id="533b4-210">Если вы вручную редактировали файл, убедитесь, что JSON хорошо определен в `manifest.json` **инструменте Манифест** приложения в App Studio.</span><span class="sxs-lookup"><span data-stu-id="533b4-210">If you manually edited the `manifest.json` file, verify that the JSON is well-defined in the **App Manifest** tool in App Studio.</span></span>

<span data-ttu-id="533b4-211">**Содержимое вкладки, которое не отображается**</span><span class="sxs-lookup"><span data-stu-id="533b4-211">**Tab content not displayed**</span></span>

<span data-ttu-id="533b4-212">Убедитесь, что приложение запущено.</span><span class="sxs-lookup"><span data-stu-id="533b4-212">Verify that your app is running.</span></span> <span data-ttu-id="533b4-213">Если это не так, перейдите к терминалу и запустите `npm start` .</span><span class="sxs-lookup"><span data-stu-id="533b4-213">If it isn't, go to the terminal and run `npm start`.</span></span>

## <a name="see-also"></a><span data-ttu-id="533b4-214">См. также</span><span class="sxs-lookup"><span data-stu-id="533b4-214">See also</span></span>

* [<span data-ttu-id="533b4-215">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="533b4-215">Prepare your Microsoft 365 tenant</span></span>](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [<span data-ttu-id="533b4-216">Выбор установки для тестирования и отлаговки приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="533b4-216">Choosing a setup to test and debug your Microsoft Teams app</span></span>](../concepts/build-and-test/debug.md)
* [<span data-ttu-id="533b4-217">Создание вкладок и других опытом работы с клиентом Microsoft Teams JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="533b4-217">Building tabs and other hosted experiences with the Microsoft Teams JavaScript client SDK</span></span>](../tabs/how-to/using-teams-client-sdk.md)
* [<span data-ttu-id="533b4-218">Подготовка к отправке AppSource</span><span class="sxs-lookup"><span data-stu-id="533b4-218">Prepare for AppSource submission</span></span>](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [<span data-ttu-id="533b4-219">Быстрая разработка приложений с помощью App Studio для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="533b4-219">Quickly develop apps with App Studio for Microsoft Teams</span></span>](../concepts/build-and-test/app-studio-overview.md)
* [<span data-ttu-id="533b4-220">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="533b4-220">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a><span data-ttu-id="533b4-221">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="533b4-221">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="533b4-222">Создание личной вкладки для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="533b4-222">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
