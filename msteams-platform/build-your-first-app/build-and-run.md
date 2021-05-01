---
title: Начало работы — сборка и запуск первого приложения
author: girliemac
description: Быстро создайте Microsoft Teams приложение, которое отображает "Hello, World!" сообщение с помощью Microsoft Teams набор средств.
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: 6c3d215a3f2c1aa89a9a2bf28aad081d98c6dc33
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101725"
---
# <a name="create-your-first-microsoft-teams-app"></a><span data-ttu-id="74023-104">Создание первого Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="74023-104">Create your first Microsoft Teams app</span></span>

<span data-ttu-id="74023-105">Этот quickstart учит вас создавать и запускать Microsoft Teams, которое отображает "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="74023-105">This quickstart teaches you to build and run Microsoft Teams app that displays "Hello, World!"</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74023-106">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="74023-106">Prerequisites</span></span>

<span data-ttu-id="74023-107">Перед началом работы [](#set-up-your-teams-development-tenant) необходимо настроить клиента Teams разработки и установить [Teams разработки.](#install-your-development-tools)</span><span class="sxs-lookup"><span data-stu-id="74023-107">Before you begin, you need to [set up your Teams development tenant](#set-up-your-teams-development-tenant) and [install your Teams development tools](#install-your-development-tools).</span></span>

### <a name="set-up-your-teams-development-tenant"></a><span data-ttu-id="74023-108">Настройка клиента Teams разработки</span><span class="sxs-lookup"><span data-stu-id="74023-108">Set up your Teams development tenant</span></span>

<span data-ttu-id="74023-109">Клиент **—** это как контейнер для организации.</span><span class="sxs-lookup"><span data-stu-id="74023-109">A **tenant** is like a container for an organization.</span></span> <span data-ttu-id="74023-110">В Teams терминов клиент — это место, где люди из этого орга-чата делятся файлами и запускают собрания.</span><span class="sxs-lookup"><span data-stu-id="74023-110">In Teams terms, a tenant is where people from that org chat, share files, and run meetings.</span></span> <span data-ttu-id="74023-111">Как разработчику необходимо, чтобы клиент перегружал и проверял Teams приложения, которые вы строите.</span><span class="sxs-lookup"><span data-stu-id="74023-111">As a developer, you need a tenant to sideload and test the Teams apps that you are building.</span></span>  

# <a name="do-not-have-a-tenant"></a>[<span data-ttu-id="74023-112">Нет клиента</span><span class="sxs-lookup"><span data-stu-id="74023-112">Do not have a tenant</span></span>](#tab/do-not-have-a-tenant)

<span data-ttu-id="74023-113">Вы можете получить бесплатную Teams тестовую учетную запись, которая включает клиента, который позволяет загрузку приложений, присоединившись к Microsoft 365 разработчика.</span><span class="sxs-lookup"><span data-stu-id="74023-113">You can get a free Teams test account, which includes a tenant that allows app sideloading, by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="74023-114">Процесс регистрации занимает примерно две минуты.</span><span class="sxs-lookup"><span data-stu-id="74023-114">The registration process takes approximately two minutes.</span></span>

<span data-ttu-id="74023-115">**Чтобы получить клиента**</span><span class="sxs-lookup"><span data-stu-id="74023-115">**To get a tenant**</span></span>

1. <span data-ttu-id="74023-116">Перейдите в [Microsoft 365 разработчика](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="74023-116">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="74023-117">Выберите **Join Now** и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="74023-117">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="74023-118">На экране Welcome выберите **настройка подписки E5.**</span><span class="sxs-lookup"><span data-stu-id="74023-118">In the Welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="74023-119">Настройка учетной записи Microsoft 365 разработчика.</span><span class="sxs-lookup"><span data-stu-id="74023-119">Set up your Microsoft 365 developer account.</span></span> 
   <span data-ttu-id="74023-120">После завершения отображается следующий экран:</span><span class="sxs-lookup"><span data-stu-id="74023-120">After you finish, the following screen appears:</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации на программу Microsoft 365 разработчика.":::

1. <span data-ttu-id="74023-122">Во входе Teams с новой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="74023-122">Sign in to Teams with your new account.</span></span>
1. <span data-ttu-id="74023-123">В клиенте Teams выберите **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="74023-123">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="74023-124">Убедитесь, что вы можете **Upload настраиваемый параметр** приложения.</span><span class="sxs-lookup"><span data-stu-id="74023-124">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="74023-125">Если вы это сделаете, это означает, что вы можете перегружать приложения.</span><span class="sxs-lookup"><span data-stu-id="74023-125">If you do, this means you can sideload apps.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, Teams вы можете загрузить пользовательское приложение.":::

# <a name="have-a-tenant"></a>[<span data-ttu-id="74023-127">Иметь клиента</span><span class="sxs-lookup"><span data-stu-id="74023-127">Have a tenant</span></span>](#tab/have-a-tenant)

<span data-ttu-id="74023-128">Если у вас уже есть клиент, убедитесь, что вы можете разгрузить приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="74023-128">If you already have a tenant, verify if you can sideload apps in Teams.</span></span>

<span data-ttu-id="74023-129">**Убедитесь, что приложения можно перегружать в сторону**</span><span class="sxs-lookup"><span data-stu-id="74023-129">**Verify that you can sideload your apps**</span></span> 

1. <span data-ttu-id="74023-130">В клиенте Teams выберите **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="74023-130">In the Teams Client, select **Apps**.</span></span> 
1.  <span data-ttu-id="74023-131">Убедитесь, что вы можете **Upload настраиваемый параметр** приложения.</span><span class="sxs-lookup"><span data-stu-id="74023-131">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="74023-132">Если вы это сделаете, это означает, что вы можете перегружать приложения.</span><span class="sxs-lookup"><span data-stu-id="74023-132">If you do, this means you can sideload apps.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, Teams вы можете загрузить пользовательское приложение.":::

---

### <a name="install-your-development-tools"></a><span data-ttu-id="74023-134">Установка средств разработки</span><span class="sxs-lookup"><span data-stu-id="74023-134">Install your development tools</span></span>

<span data-ttu-id="74023-135">Чтобы создать это приложение, вы будете использовать Teams набор средств для Visual Studio Code для быстрого начала работы.</span><span class="sxs-lookup"><span data-stu-id="74023-135">To build this app, you'll use the Teams Toolkit for Visual Studio Code to quickly get started.</span></span> <span data-ttu-id="74023-136">Вы также можете создавать Teams с помощью любого из ваших заранее установленных средств.</span><span class="sxs-lookup"><span data-stu-id="74023-136">You can also build Teams apps with any of your preffered tools.</span></span> 

> [!NOTE]
> <span data-ttu-id="74023-137">Teams отображает содержимое приложения только с помощью подключений HTTPS.</span><span class="sxs-lookup"><span data-stu-id="74023-137">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="74023-138">Чтобы отламыть определенные типы приложений локально, например бот, вы узнаете, как использовать ngrok для запуска безопасного туннеля между Teams и вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="74023-138">To debug certain types of apps locally, such as a bot, you'll learn how to use ngrok to set up a secure tunnel between Teams and your app.</span></span>
> 
> <span data-ttu-id="74023-139">Производственные Teams приложения находятся в облаке.</span><span class="sxs-lookup"><span data-stu-id="74023-139">Production Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="74023-140">**Установка Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="74023-140">**To install Microsoft Teams tools**</span></span>

1. <span data-ttu-id="74023-141">Установите [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="74023-141">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="74023-142">Если вы планируете создать расширение бота или обмена сообщениями, установите [ngrok](https://ngrok.com/download) и выставите локальный интернет с помощью [ngrok.](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok)</span><span class="sxs-lookup"><span data-stu-id="74023-142">If you plan to build a bot or messaging extension, install [ngrok](https://ngrok.com/download) and [expose your localhost to the Internet using ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok).</span></span>
1. <span data-ttu-id="74023-143">Установка последней версии [Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="74023-143">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="74023-144">Набор инструментов не поддерживает более ранние версии Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="74023-144">The toolkit does not support earlier versions of Visual Studio Code.</span></span>

1. В левой панели действий выберите **Расширения.** :::image type="icon" source="../assets/icons/vs-code-extensions.png":::
1. <span data-ttu-id="74023-146">В **Microsoft Teams набор средств** выберите **Установите**.</span><span class="sxs-lookup"><span data-stu-id="74023-146">In **Microsoft Teams Toolkit**, select **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Иллюстрация, показывающая, Visual Studio Code в Visual Studio Code можно установить Microsoft Teams набор средств расширения.":::

## <a name="1-create-your-app-project"></a><span data-ttu-id="74023-148">1. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="74023-148">1. Create your app project</span></span>

1. <span data-ttu-id="74023-149">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="74023-149">Open Visual Studio Code.</span></span>
1. Выберите **Microsoft Teams набор средств** :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **создать новое приложение Teams.**

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="Снимок экрана, показывающий, как создать проект приложения с помощью Visual Studio Code Teams набор средств.":::
   
1. <span data-ttu-id="74023-152">Во входе в Microsoft 365 учетную запись разработки.</span><span class="sxs-lookup"><span data-stu-id="74023-152">Sign in with your Microsoft 365 development account.</span></span> <span data-ttu-id="74023-153">Либо только что созданная учетная запись, либо уже созданная учетная запись, которая позволяет загрузку приложения в сторону.</span><span class="sxs-lookup"><span data-stu-id="74023-153">Either the one you just created or the account you already had that allows app sideloading.</span></span>
1. <span data-ttu-id="74023-154">На экране **Выберите проект** перейдите в приложение **Personal и** выберите **JS** (JavaScript) > **Далее**.</span><span class="sxs-lookup"><span data-stu-id="74023-154">On the **Select project** screen, go to **Personal app** and select **JS** (JavaScript) > **Next**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Снимок экрана, показывающий, как настроить проект приложения с помощью Visual Studio Code Teams набор средств.":::

1. <span data-ttu-id="74023-156">Введите имя для Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="74023-156">Enter a name for your Teams app.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="Снимок экрана, показывающий, как добавить имя в проект приложения с помощью Visual Studio Code Teams набор средств.":::

1. <span data-ttu-id="74023-158">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="74023-158">Select **Finish**.</span></span> 
   <span data-ttu-id="74023-159">Теперь проект настроен.</span><span class="sxs-lookup"><span data-stu-id="74023-159">Your project is now configured.</span></span> 

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="74023-160">2. Понимание компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="74023-160">2. Understand your app project components</span></span>

<span data-ttu-id="74023-161">После того как набор инструментов настроит проект приложения, у вас будут компоненты для создания "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="74023-161">After the toolkit configures your app project, you have the components to build your "Hello, World!"</span></span> <span data-ttu-id="74023-162">Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="74023-162">Teams app.</span></span> <span data-ttu-id="74023-163">Каталоги и файлы проекта находятся в Visual Studio Code Explorer.</span><span class="sxs-lookup"><span data-stu-id="74023-163">The project's directories and files are located in the Visual Studio Code Explorer.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="Снимок экрана, показывающий леса в проекте приложения с помощью Visual Studio Code Teams набор средств.":::

<span data-ttu-id="74023-165">Набор инструментов автоматически создает строительные леса приложений в каталоге на основе возможностей, добавленных `src` во время установки.</span><span class="sxs-lookup"><span data-stu-id="74023-165">The toolkit automatically creates app scaffolding in the `src` directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="74023-166">Так как вы создали вкладку во время настройки, файл в каталоге обрабатывает инициализацию и `App.js` `src/components` маршрутизацию приложения.</span><span class="sxs-lookup"><span data-stu-id="74023-166">Since you created a tab during setup, the `App.js` file in the `src/components` directory handles the initialization and routing of your app.</span></span> <span data-ttu-id="74023-167">Файл также вызывает SDK Microsoft Teams JavaScript, чтобы установить связь между вашим приложением и Teams.</span><span class="sxs-lookup"><span data-stu-id="74023-167">The file also calls the Microsoft Teams JavaScript client SDK to establish communication between your app and Teams.</span></span> 

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="74023-168">3. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="74023-168">3. Build and run your app</span></span>

<span data-ttu-id="74023-169">Создайте и запустите приложение локально, чтобы сэкономить время.</span><span class="sxs-lookup"><span data-stu-id="74023-169">Build and run your app locally to save time.</span></span> 

<span data-ttu-id="74023-170">**Создание и запуск приложения**</span><span class="sxs-lookup"><span data-stu-id="74023-170">**To build and run your app**</span></span>

1. <span data-ttu-id="74023-171">В Visual Studio Code выберите **View**  >  **Terminal**.</span><span class="sxs-lookup"><span data-stu-id="74023-171">In Visual Studio Code, select **View** > **Terminal**.</span></span>
1. <span data-ttu-id="74023-172">Запуск `npm install` .</span><span class="sxs-lookup"><span data-stu-id="74023-172">Run `npm install`.</span></span>
1. <span data-ttu-id="74023-173">Запуск `npm start` .</span><span class="sxs-lookup"><span data-stu-id="74023-173">Run `npm start`.</span></span>
  
  <span data-ttu-id="74023-174">**Компилировать успешно!**</span><span class="sxs-lookup"><span data-stu-id="74023-174">A **Compiled successfully!**</span></span> <span data-ttu-id="74023-175">сообщение отображается в терминале.</span><span class="sxs-lookup"><span data-stu-id="74023-175">message appears in the terminal.</span></span> <span data-ttu-id="74023-176">Ваше приложение теперь работает на локальном сайте по `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="74023-176">Your app is now running on your localhost at `https://localhost:3000`.</span></span> 

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="74023-177">4. В Teams</span><span class="sxs-lookup"><span data-stu-id="74023-177">4. Sideload your app in Teams</span></span>

<span data-ttu-id="74023-178">Sideloading — это процесс установки приложения в Teams, которое не было утверждено вашим администратором или Корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="74023-178">Sideloading is the process of installing an app in Teams that hasn't been approved by your admin or Microsoft.</span></span> <span data-ttu-id="74023-179">При тестировании и отладке приложений часто используется Teams загрузка.</span><span class="sxs-lookup"><span data-stu-id="74023-179">Sideloading is common when testing and debugging Teams apps.</span></span>

<span data-ttu-id="74023-180">По умолчанию Teams не разрешает загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="74023-180">By default, Teams doesn't allow app sideloading.</span></span> <span data-ttu-id="74023-181">Этот параметр можно изменить в центре Teams администратора.</span><span class="sxs-lookup"><span data-stu-id="74023-181">You can change this setting in the Teams admin center.</span></span>

<span data-ttu-id="74023-182">**Чтобы включить загрузку приложений в Teams**</span><span class="sxs-lookup"><span data-stu-id="74023-182">**To enable app sideloading in Teams**</span></span>

1. <span data-ttu-id="74023-183">Вопишитесь в [центр администрирования Microsoft 365 с](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="74023-183">Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>  
1. <span data-ttu-id="74023-184">Выберите **Показать все**  >  **Teams**.</span><span class="sxs-lookup"><span data-stu-id="74023-184">Select **Show All** > **Teams**.</span></span> 

   ![изображение меню центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > <span data-ttu-id="74023-186">Для появления параметра Teams может занять **до 24** часов.</span><span class="sxs-lookup"><span data-stu-id="74023-186">It can take up to 24 hours for the **Teams** option to appear.</span></span> 

1. <span data-ttu-id="74023-187">Перейдите **Teams политики** установки приложений  >    >  **Global** (по умолчанию в масштабах всей Организации).</span><span class="sxs-lookup"><span data-stu-id="74023-187">Go to **Teams apps** > **Setup policies** > **Global** (Org-wide default).</span></span>

   ![включить представление боковой нагрузки](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. <span data-ttu-id="74023-189">Включите **переключить настраиваемые приложения** для загрузки.</span><span class="sxs-lookup"><span data-stu-id="74023-189">Turn on the **upload custom apps** toggle.</span></span>

1. <span data-ttu-id="74023-190">Выберите **Сохранить,** чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="74023-190">Select **Save** to save the changes.</span></span>

   <span data-ttu-id="74023-191">Клиент тестового клиента теперь разрешает настраиваемую загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="74023-191">Your test tenant now allows custom app sideloading.</span></span>

   > [!Note]
   > <span data-ttu-id="74023-192">Проверьте проблемы перед загрузкой приложения с помощью функции проверки в App Studio, которая входит в набор инструментов.</span><span class="sxs-lookup"><span data-stu-id="74023-192">Check for issues before sideloading your app using the validation feature in App Studio, which is included in the toolkit.</span></span> <span data-ttu-id="74023-193">Устранение ошибок для успешной загрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="74023-193">Fix the errors to successfully sideload the app.</span></span>


### <a name="sideload-your-app"></a><span data-ttu-id="74023-194">Боковая загрузка приложения</span><span class="sxs-lookup"><span data-stu-id="74023-194">Sideload your app</span></span>

1. <span data-ttu-id="74023-195">В Visual Studio Code откройте Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="74023-195">In Visual Studio Code, open the Teams Toolkit.</span></span>
1. <span data-ttu-id="74023-196">Перейдите в **App Studio**.</span><span class="sxs-lookup"><span data-stu-id="74023-196">Go to **App Studio**.</span></span>  
1. <span data-ttu-id="74023-197">Выберите **тест и раздайте**  >  **установку.**</span><span class="sxs-lookup"><span data-stu-id="74023-197">Select **Test and Distribute** > **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="Снимок экрана, показывающий, как Teams для клиента с помощью Visual Studio Code Teams набор средств.":::

<span data-ttu-id="74023-199">**В качестве альтернативы**</span><span class="sxs-lookup"><span data-stu-id="74023-199">**Alternatively**</span></span>

1. <span data-ttu-id="74023-200">Выберите **клавишу F5,** чтобы открыть окно браузера для установки.</span><span class="sxs-lookup"><span data-stu-id="74023-200">Select the **F5** key to open browser window to install.</span></span> <span data-ttu-id="74023-201">Это позволит пропустить процесс установки в **App Studio** и Teams в браузере.</span><span class="sxs-lookup"><span data-stu-id="74023-201">This will skip the installation process in the **App Studio** and lauch Teams in your browser.</span></span>
1. <span data-ttu-id="74023-202">В диалоговом окте установки выберите **Добавить,** чтобы установить приложение для Teams.</span><span class="sxs-lookup"><span data-stu-id="74023-202">In the installation dialog, select **Add** to install your app to Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="Снимок экрана, показывающий, как перегрузить приложение в Teams клиента.":::

   > [!Note]
   > <span data-ttu-id="74023-204">App Studio также доступен в качестве отдельного приложения для Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="74023-204">App Studio is also available as a stand-alone app for Teams client.</span></span>

### <a name="troubleshoot-sideloading-issues"></a><span data-ttu-id="74023-205">Устранение неполадок при перегрузке</span><span class="sxs-lookup"><span data-stu-id="74023-205">Troubleshoot sideloading issues</span></span>

<span data-ttu-id="74023-206">**Сбой установки**</span><span class="sxs-lookup"><span data-stu-id="74023-206">**Installation failed**</span></span>

<span data-ttu-id="74023-207">Если сообщение об ошибке появляется при установке приложения, убедитесь, что сведения о приложении правильно `Manifest parsing has failed` введены.</span><span class="sxs-lookup"><span data-stu-id="74023-207">If the `Manifest parsing has failed` error message appears while installing your app, verify that the app information is correctly entered.</span></span>

<span data-ttu-id="74023-208">**Проверка сведений о приложении**</span><span class="sxs-lookup"><span data-stu-id="74023-208">**To verify the app information**</span></span>

* <span data-ttu-id="74023-209">В Teams набор средств перейдите в **App Studio** App и убедитесь, что вся необходимая информация введена  >   правильно.</span><span class="sxs-lookup"><span data-stu-id="74023-209">In the Teams Toolkit, go to **App Studio** > **App details** and verify that all the required information is correctly entered.</span></span>
*  <span data-ttu-id="74023-210">Если вы вручную редактировали файл, убедитесь, что JSON хорошо определен в `manifest.json` **инструменте Манифест** приложения в App Studio.</span><span class="sxs-lookup"><span data-stu-id="74023-210">If you manually edited the `manifest.json` file, verify that the JSON is well-defined in the **App Manifest** tool in App Studio.</span></span>

<span data-ttu-id="74023-211">**Содержимое вкладки, которое не отображается**</span><span class="sxs-lookup"><span data-stu-id="74023-211">**Tab content not displayed**</span></span>

<span data-ttu-id="74023-212">Убедитесь, что приложение запущено.</span><span class="sxs-lookup"><span data-stu-id="74023-212">Verify that your app is running.</span></span> <span data-ttu-id="74023-213">Если это не так, перейдите к терминалу и запустите `npm start` .</span><span class="sxs-lookup"><span data-stu-id="74023-213">If it isn't, go to the terminal and run `npm start`.</span></span>

## <a name="see-also"></a><span data-ttu-id="74023-214">См. также</span><span class="sxs-lookup"><span data-stu-id="74023-214">See also</span></span>

* [<span data-ttu-id="74023-215">Подготовка клиента Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="74023-215">Prepare your Microsoft 365 tenant</span></span>](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [<span data-ttu-id="74023-216">Выбор установки для тестирования и отлаговки Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="74023-216">Choosing a setup to test and debug your Microsoft Teams app</span></span>](../concepts/build-and-test/debug.md)
* [<span data-ttu-id="74023-217">Создание вкладок и других опытом работы с клиентом Microsoft Teams JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="74023-217">Building tabs and other hosted experiences with the Microsoft Teams JavaScript client SDK</span></span>](../tabs/how-to/using-teams-client-sdk.md)
* [<span data-ttu-id="74023-218">Подготовка к отправке AppSource</span><span class="sxs-lookup"><span data-stu-id="74023-218">Prepare for AppSource submission</span></span>](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [<span data-ttu-id="74023-219">Быстрая разработка приложений с помощью App Studio для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="74023-219">Quickly develop apps with App Studio for Microsoft Teams</span></span>](../concepts/build-and-test/app-studio-overview.md)
* [<span data-ttu-id="74023-220">Создание вкладки канала</span><span class="sxs-lookup"><span data-stu-id="74023-220">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a><span data-ttu-id="74023-221">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="74023-221">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="74023-222">Создайте личную вкладку для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="74023-222">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
