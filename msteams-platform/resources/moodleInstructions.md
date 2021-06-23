---
title: Установка Moodle LMS
description: Установка и настройка приложения интеграции Moodle для Microsoft Teams
keywords: Teams Плагины интеграции приложений Moodle
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 54f4fec4e240f866c686ed715bd5093a319a2a48
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069173"
---
# <a name="install-moodle-lms"></a><span data-ttu-id="3d71b-104">Установка Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="3d71b-104">Install Moodle LMS</span></span>

<span data-ttu-id="3d71b-105">В этой статье вы узнаете, как установить Moodle LMS.</span><span class="sxs-lookup"><span data-stu-id="3d71b-105">In this article you'll learn how to install the Moodle LMS.</span></span>

> [!NOTE]
> <span data-ttu-id="3d71b-106">Чтобы помочь ИТ-администраторам легко настроить интеграцию Moodle и Teams, Microsoft 365 плагины Moodle обновляются для следующих версий:</span><span class="sxs-lookup"><span data-stu-id="3d71b-106">To help IT admins to easily set-up Moodle and Teams integration, open-source Microsoft 365 Moodle Plugins is updated for the following:</span></span>
>
> * <span data-ttu-id="3d71b-107">Авторегистрация сервера Moodle с [помощью Azure Active Directory (Azure AD).](https://azure.microsoft.com/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="3d71b-107">Auto-registration of your Moodle server with [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).</span></span>
>
> * <span data-ttu-id="3d71b-108">Одним щелчком мыши развертывание бота помощника Moodle в Azure.</span><span class="sxs-lookup"><span data-stu-id="3d71b-108">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
>
> * <span data-ttu-id="3d71b-109">Автозапранение команд и автохронизация регистраций команд для всех или выбор курсов Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-109">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
>
> * <span data-ttu-id="3d71b-110">Автоматическая установка вкладки Moodle и бота помощника Moodle в каждую синхронизированную команду.</span><span class="sxs-lookup"><span data-stu-id="3d71b-110">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>
>
> <span data-ttu-id="3d71b-111">Дополнительные данные о возможностях, которые предоставляет эта интеграция, см. в [Microsoft Teams и Moodle.](https://education.microsoft.com/resource/3dffb3a8)</span><span class="sxs-lookup"><span data-stu-id="3d71b-111">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d71b-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3d71b-112">Prerequisites</span></span>

<span data-ttu-id="3d71b-113">Ниже следующую предпосылку для установки Moodle:</span><span class="sxs-lookup"><span data-stu-id="3d71b-113">Following are the prerequisites to install Moodle:</span></span>

* <span data-ttu-id="3d71b-114">Учетные данные администратора Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-114">Moodle administrator credentials.</span></span>

* <span data-ttu-id="3d71b-115">Учетные данные администратора Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d71b-115">Azure AD administrator credentials.</span></span>

* <span data-ttu-id="3d71b-116">Подписка Azure, в которой можно создавать новые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3d71b-116">An Azure subscription where you can create new resources.</span></span>

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="3d71b-117">1. Установка Microsoft 365 плагинов Moodle</span><span class="sxs-lookup"><span data-stu-id="3d71b-117">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="3d71b-118">Интеграция Moodle Microsoft Teams в Microsoft Teams питания с открытым исходным кодом Microsoft 365 [плагинов Moodle](https://github.com/Microsoft/o365-moodle).</span><span class="sxs-lookup"><span data-stu-id="3d71b-118">Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugins set](https://github.com/Microsoft/o365-moodle).</span></span>

### <a name="requisite-applications-and-plugins"></a><span data-ttu-id="3d71b-119">Необходимые приложения и плагины</span><span class="sxs-lookup"><span data-stu-id="3d71b-119">Requisite applications and plugins</span></span>

<span data-ttu-id="3d71b-120">Убедитесь, что перед началом работы с установкой Microsoft 365 плагинов Moodle необходимо установить и скачать следующее:</span><span class="sxs-lookup"><span data-stu-id="3d71b-120">Ensure to install and download the following before proceeding with the Microsoft 365 Moodle plugins installation:</span></span>

1. <span data-ttu-id="3d71b-121">Убедитесь, что [установить текущую стабильную версию Moodle](https://download.moodle.org/releases/latest/).</span><span class="sxs-lookup"><span data-stu-id="3d71b-121">Ensure to install a [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="3d71b-122">Скачайте и сохраните плагины Moodle [OpenID Подключение](https://moodle.org/plugins/auth_oidc) и [Microsoft 365 интеграции](https://moodle.org/plugins/local_o365) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3d71b-122">Download and save the Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins to your local computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3d71b-123">Установка плагинов OpenID Подключение и Microsoft 365 интеграции требуется для Teams интеграции.</span><span class="sxs-lookup"><span data-stu-id="3d71b-123">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span>
    >
    > <span data-ttu-id="3d71b-124">Кроме того, [рекомендуется использовать Microsoft 365 Teams темы.](https://moodle.org/plugins/theme_boost_o365teams)</span><span class="sxs-lookup"><span data-stu-id="3d71b-124">In addition, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugins is highly recommended.</span></span>

### <a name="microsoft-365-moodle-plugins"></a><span data-ttu-id="3d71b-125">Microsoft 365 Плагины Moodle</span><span class="sxs-lookup"><span data-stu-id="3d71b-125">Microsoft 365 Moodle plugins</span></span>

1. <span data-ttu-id="3d71b-126">Вопишитесь на сервер Moodle в  качестве администратора и выберите администрирование сайта из Параметры, расположенного в левой панели навигации. [](https://docs.moodle.org/22/en/Settings_block)</span><span class="sxs-lookup"><span data-stu-id="3d71b-126">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="3d71b-127">Выберите **вкладку Plugins,** а затем установите **плагины Install.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-127">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="3d71b-128">В разделе **Установка плагинов из файла ZIP** выберите выберите **файл.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-128">From the **Install plugins from ZIP file** section, select **Choose a file**.</span></span>

1. <span data-ttu-id="3d71b-129">Выберите **Upload** файл из левой панели навигации, просмотрите скачаный файл и **Upload файл**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-129">Select **Upload a file** option from the left navigation panel, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="3d71b-130">Выберите **администрирование сайта** из левой панели навигации, чтобы вернуться на панель мониторинга администрирования.</span><span class="sxs-lookup"><span data-stu-id="3d71b-130">Select **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="3d71b-131">Прокрутите вниз **к локальным плагинам** и **выберите ссылку Microsoft 365 интеграции.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-131">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span>

    > [!IMPORTANT]
    >
    > * <span data-ttu-id="3d71b-132">Откройте страницу конфигурации Microsoft 365 Moodle Plugins на отдельной вкладке браузера, так как вам необходимо вернуться к этому набору страниц на протяжении всего процесса.</span><span class="sxs-lookup"><span data-stu-id="3d71b-132">Keep your Microsoft 365 Moodle Plugins configuration page open in a separate browser tab as you need to return to this set of pages throughout the process.</span></span>  
    >
    > * <span data-ttu-id="3d71b-133">Если у вас нет существующего сайта Moodle, перейдите в [Moodle на репо Azure](https://github.com/azure/moodle) и быстро разверните экземпляр Moodle и настройте его под ваши нужды.</span><span class="sxs-lookup"><span data-stu-id="3d71b-133">If you do not have an existing Moodle site, go to the [Moodle on Azure](https://github.com/azure/moodle) repo, and quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a><span data-ttu-id="3d71b-134">2. Настройка подключения между плагинами Microsoft 365 и Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="3d71b-134">2. Configure the connection between the Microsoft 365 plugins and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="3d71b-135">Необходимо настроить подключение между плагинами Microsoft 365 Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d71b-135">You must configure the connection between the Microsoft 365 plugins and Azure AD.</span></span>

### <a name="requisites"></a><span data-ttu-id="3d71b-136">Реквизиты</span><span class="sxs-lookup"><span data-stu-id="3d71b-136">Requisites</span></span>

<span data-ttu-id="3d71b-137">Зарегистрируйте Moodle в качестве приложения в Azure AD с помощью сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d71b-137">Register Moodle as an application in your Azure AD, using the PowerShell script.</span></span> <span data-ttu-id="3d71b-138">Сценарий Powershell содержит следующее:</span><span class="sxs-lookup"><span data-stu-id="3d71b-138">The Powershell script provisions the following:</span></span>

* <span data-ttu-id="3d71b-139">Новое приложение Azure AD для Microsoft 365 клиента, которое используется Microsoft 365 Плагины Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-139">A new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugins.</span></span>
* <span data-ttu-id="3d71b-140">Приложение для клиента Microsoft 365, настройка URL-адресов и разрешений на необходимый ответ для предварительного приложения, а также `AppID` возвращает и `Key` .</span><span class="sxs-lookup"><span data-stu-id="3d71b-140">The app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and returns the `AppID` and `Key`.</span></span>

<span data-ttu-id="3d71b-141">Используйте созданную и на Microsoft 365 страницу настройки плагинов Moodle для настройки сайта сервера `AppID` `Key` Moodle с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d71b-141">Use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugins setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="3d71b-142">Сценарий PowerShell не обновляется с последними элементами конфигурации, поэтому необходимо выполнить конфигурацию вручную после действий, описанных на страницах выпуска Moodle [3.8.0.4 и 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) и [3.8.0.5 и 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release)</span><span class="sxs-lookup"><span data-stu-id="3d71b-142">The PowerShell script is not updated with the latest configuration items, therefore, you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span>
>
> * <span data-ttu-id="3d71b-143">Дополнительные сведения о регистрации экземпляра Moodle вручную см. в статью Регистрация экземпляра [Moodle в качестве приложения.](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)</span><span class="sxs-lookup"><span data-stu-id="3d71b-143">For more information on registering your Moodle instance manually, see [Register your Moodle instance as an application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="3d71b-144">Вкладка Moodle для Microsoft Teams потока информации</span><span class="sxs-lookup"><span data-stu-id="3d71b-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="3d71b-145">На странице Microsoft 365 интеграции выберите вкладку **Setup.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-145">From the Microsoft 365 Integration plugins page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="3d71b-146">Выберите **кнопку Download PowerShell Script** и сохраните ее в качестве папки ZIP на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3d71b-146">Select the **Download PowerShell Script** button and save it as a ZIP folder to your local computer.</span></span>

1. <span data-ttu-id="3d71b-147">Подготовка сценария PowerShell из файла ZIP следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3d71b-147">Prepare the PowerShell script from the ZIP file as follows:</span></span> 

    1. <span data-ttu-id="3d71b-148">Скачайте и извлекайте `Moodle-AzureAD-Powershell.zip` файл.</span><span class="sxs-lookup"><span data-stu-id="3d71b-148">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="3d71b-149">Откройте извлеченную папку.</span><span class="sxs-lookup"><span data-stu-id="3d71b-149">Open the extracted folder.</span></span>
    1. <span data-ttu-id="3d71b-150">Щелкните правой кнопкой мыши `Moodle-AzureAD-Script.ps1` по файлу и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-150">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="3d71b-151">На **вкладке General** в окне Свойства выберите почтовый ящик рядом с атрибутом Security, расположенным в `Unblock` нижней части окна. </span><span class="sxs-lookup"><span data-stu-id="3d71b-151">Under the **General** tab of the Properties window, select the `Unblock` checkbox next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="3d71b-152">Нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-152">Select **OK**.</span></span>
    1. <span data-ttu-id="3d71b-153">Скопируйте путь каталога в извлеченную папку.</span><span class="sxs-lookup"><span data-stu-id="3d71b-153">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="3d71b-154">Запустите PowerShell в качестве администратора:</span><span class="sxs-lookup"><span data-stu-id="3d71b-154">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="3d71b-155">Выберите «Начать».</span><span class="sxs-lookup"><span data-stu-id="3d71b-155">Select Start.</span></span>
    1. <span data-ttu-id="3d71b-156">Тип PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d71b-156">Type PowerShell.</span></span>
    1. <span data-ttu-id="3d71b-157">Щелкните правой **кнопкой мыши Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-157">Right-click on **Windows PowerShell**.</span></span>
    1. <span data-ttu-id="3d71b-158">Выберите **Выполнить в качестве администратора.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-158">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="3d71b-159">Перейдите к unzipped каталогу, введя в текст `cd .../.../Moodle-AzureAD-Powershell` `.../...` путь к каталогу.</span><span class="sxs-lookup"><span data-stu-id="3d71b-159">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="3d71b-160">Выполните сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3d71b-160">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="3d71b-161">Введите `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .</span><span class="sxs-lookup"><span data-stu-id="3d71b-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="3d71b-162">Введите `./Moodle-AzureAD-Script.ps1` .</span><span class="sxs-lookup"><span data-stu-id="3d71b-162">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="3d71b-163">Вопишитесь в Microsoft 365 учетную запись администратора в всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="3d71b-163">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="3d71b-164">Введите имя приложения Azure AD, например, плагинов Moodle или Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-164">Enter the name of the Azure AD Application, for example, Moodle or Moodle plugins.</span></span>
    1. <span data-ttu-id="3d71b-165">Введите URL-адрес сервера Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-165">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="3d71b-166">**Скопируйте ID приложения `AppID` ()** и **ключ `Key` приложения(),** созданный скриптом, и сохраните их.</span><span class="sxs-lookup"><span data-stu-id="3d71b-166">Copy the **Application ID (`AppID`)** and **Application Key(`Key`)** generated by the script and save them.</span></span>

1. <span data-ttu-id="3d71b-167">Далее необходимо добавить и добавить в Microsoft 365 `AppID` `Key` плагины Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-167">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugins.</span></span> <span data-ttu-id="3d71b-168">Возвращайся на страницу администрирования плагинов, администрирование > плагинов > Microsoft 365 интеграции.</span><span class="sxs-lookup"><span data-stu-id="3d71b-168">Return to the plugins administration page, Site administration > Plugins > Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="3d71b-169">На **вкладке Установка** добавьте скопированную ранее и выберите `AppID` сохранить `Key` **изменения.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-169">On the **Setup** tab add the `AppID` and `Key` you copied previously, and then select **Save changes**.</span></span> <span data-ttu-id="3d71b-170">После обновления страницы можно увидеть новый раздел **Выбор метода подключения.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-170">After the page refreshes, you can see a new section **Choose connection method**.</span></span>

1. <span data-ttu-id="3d71b-171">В **методе Выбор подключения** выберите почтовый ящик с меткой **По** умолчанию, а затем снова выберите **Сохранить изменения.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-171">In the **Choose connection method**, select the checkbox labeled **Default**, and then select **Save changes** again.</span></span>

1. <span data-ttu-id="3d71b-172">После обновления страницы вы можете увидеть еще один новый раздел **Согласие администратора & дополнительные сведения**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-172">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="3d71b-173">Выберите **ссылку Предоставление** согласия администратора, введите Microsoft 365  учетные данные глобального администратора, а затем примите решение о предоставлении разрешений.</span><span class="sxs-lookup"><span data-stu-id="3d71b-173">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="3d71b-174">Рядом с **полем Клиент Azure AD выберите** кнопку **Обнаружение.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-174">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="3d71b-175">Рядом с **URL-адресом OneDrive для бизнеса** выберите кнопку **Обнаружение.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-175">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="3d71b-176">После заполнения полей снова выберите кнопку **Сохранить изменения.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-176">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="3d71b-177">Выберите **кнопку Обновление** для проверки установки, а затем выберите **сохранить изменения.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-177">Select the **Update** button to verify the installation, and then select **Save changes**.</span></span>

1. <span data-ttu-id="3d71b-178">Синхронизация пользователей между сервером Moodle и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d71b-178">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="3d71b-179">Для начала сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3d71b-179">To get started:</span></span>

    > [!NOTE]
    > <span data-ttu-id="3d71b-180">В зависимости от среды можно выбрать различные параметры на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="3d71b-180">Depending on your environment, you can select different options during this stage.</span></span>

1. <span data-ttu-id="3d71b-181">Синхронизация пользователей между сервером Moodle и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d71b-181">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="3d71b-182">В зависимости от среды можно выбрать различные параметры на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="3d71b-182">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="3d71b-183">Для начала сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3d71b-183">To get started:</span></span>
    1. <span data-ttu-id="3d71b-184">Переключиться на **вкладку Sync Параметры .**</span><span class="sxs-lookup"><span data-stu-id="3d71b-184">Switch to the **Sync Settings tab**.</span></span>

    1. <span data-ttu-id="3d71b-185">В разделе **Синхронизация пользователей с azure AD** выберите почтовые ящики, применимые к вашей среде.</span><span class="sxs-lookup"><span data-stu-id="3d71b-185">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="3d71b-186">Необходимо выбрать следующее:</span><span class="sxs-lookup"><span data-stu-id="3d71b-186">You must select the following:</span></span>  

        <span data-ttu-id="3d71b-187">✔ создать учетные записи в Moodle для пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d71b-187">✔ Create accounts in Moodle for users in Azure AD.</span></span>

        <span data-ttu-id="3d71b-188">✔ обновления всех учетных записей в Moodle для пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d71b-188">✔ Update all accounts in Moodle for users in Azure AD.</span></span>

    1. <span data-ttu-id="3d71b-189">В разделе **Ограничение создания** пользователей можно настроить фильтр, чтобы ограничить пользователей Azure AD, синхронизированных с Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-189">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="3d71b-190">Раздел **Сопоставление полей** пользователя позволяет настроить отображение поля Azure AD для сопоставления профилей пользователей Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-190">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="3d71b-191">В разделе **Teams Синхронизация** можно выбрать для автоматического создания групп, например групп для некоторых или всех существующих курсов Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-191">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

13. <span data-ttu-id="3d71b-192">Чтобы проверить [задания cron](https://docs.moodle.org/310/en/Cron) и выполнить их вручную  для первого запуска, выберите ссылку на страницу управления запланированными задачами в разделе Синхронизация пользователей **с azure AD.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-192">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="3d71b-193">В этом случае вы **перенабирались на страницу Запланированные** задачи.</span><span class="sxs-lookup"><span data-stu-id="3d71b-193">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="3d71b-194">Прокрутите вниз и найдите пользователей **Sync с заданием Azure AD** и выберите **Выполнить сейчас.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-194">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="3d71b-195">Если вы выберете для создания групп на основе существующих курсов, вы также можете запустить группы пользователей **в Microsoft 365** задания.</span><span class="sxs-lookup"><span data-stu-id="3d71b-195">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="3d71b-196">Cron [](https://docs.moodle.org/310/en/Cron) Moodle выполняется в соответствии с расписанием задач.</span><span class="sxs-lookup"><span data-stu-id="3d71b-196">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="3d71b-197">Расписание по умолчанию — один раз в день.</span><span class="sxs-lookup"><span data-stu-id="3d71b-197">The default schedule is once a day.</span></span> <span data-ttu-id="3d71b-198">Тем не менее, крона должна работать чаще, чтобы сохранить все в синхронизации.</span><span class="sxs-lookup"><span data-stu-id="3d71b-198">However, the cron must run more frequently to keep everything in sync.</span></span>

1. <span data-ttu-id="3d71b-199">Вернись на страницу администрирования плагинов, администрирование **> плагинов**> Microsoft 365 интеграции и выберите **Teams Параметры** страницу.</span><span class="sxs-lookup"><span data-stu-id="3d71b-199">Return to the plugins administration page, **Site administration > Plugins > Microsoft 365 Integration**, and select the **Teams Settings** page.</span></span>

1. <span data-ttu-id="3d71b-200">На **Teams Параметры** настроить необходимые параметры, чтобы включить интеграцию Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="3d71b-200">On the **Teams Settings** page, configure the required settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="3d71b-201">Чтобы включить **openID Подключение,** выберите ссылку **Управление** проверкой подлинности и выберите значок глаза в строке **OpenId Подключение,** если она серым цветом.</span><span class="sxs-lookup"><span data-stu-id="3d71b-201">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="3d71b-202">Чтобы включить встраив кадр, выберите **ссылку HTTP Security,** а затем выберите почтовый ящик рядом с разрешить встраивку **кадров.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-202">To enable frame embedding, select the **HTTP Security** link, and then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="3d71b-203">Чтобы включить веб-службы, которые позволяют функции API Moodle, выберите ссылку **Расширенные** функции, а затем убедитесь, что рядом с почтовым ящиком Включить веб-службы выбраны. </span><span class="sxs-lookup"><span data-stu-id="3d71b-203">To enable web services, which enables the Moodle API features, select the **Advanced Features** link, and then ensure the checkbox next to **Enable web services** is selected.</span></span>
    1. <span data-ttu-id="3d71b-204">Чтобы включить внешние службы для Microsoft 365, выберите ссылку **Внешние** службы, а затем:</span><span class="sxs-lookup"><span data-stu-id="3d71b-204">To enable the external services for Microsoft 365, select the **External services** link, and then:</span></span>  

        <span data-ttu-id="3d71b-205">✔ **Выберите изменение** в строке **Moodle Microsoft 365 Webservices.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-205">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>

        <span data-ttu-id="3d71b-206">✔ выберите контрольный ящик рядом с **включенной,** а затем выберите **Сохранить изменения**</span><span class="sxs-lookup"><span data-stu-id="3d71b-206">✔ Select the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="3d71b-207">Отредактировать разрешения пользователя, проверку подлинности, чтобы разрешить им создавать маркеры веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3d71b-207">Edit your authenticated user permissions to allow them to create web service tokens.</span></span>

        <span data-ttu-id="3d71b-208">✔ выберите ссылку пользователя **на роль** редактирования.</span><span class="sxs-lookup"><span data-stu-id="3d71b-208">✔ Select the **Editing role Authenticated user** link.</span></span>

        <span data-ttu-id="3d71b-209">✔ прокрутите вниз и найдите возможность **создания** маркера веб-службы и выберите контрольный ящик **Разрешить.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-209">✔ Scroll down and find the **Create a web service token** capability and select the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="3d71b-210">3. Развертывание бота помощника Moodle в Azure</span><span class="sxs-lookup"><span data-stu-id="3d71b-210">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="3d71b-211">Бесплатный бот помощника Moodle для Microsoft Teams помогает преподавателям и учащимся отвечать на вопросы о своих курсах, заданиях, оценках и других сведениях в Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-211">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades, and other information in Moodle.</span></span> <span data-ttu-id="3d71b-212">Бот также отправляет уведомления Moodle учащимся и преподавателям в Teams.</span><span class="sxs-lookup"><span data-stu-id="3d71b-212">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="3d71b-213">Бот — это проект с открытым исходным кодом, поддерживаемый Корпорацией Майкрософт, и доступен в [GitHub.](https://github.com/microsoft/Moodle-Teams-Bot)</span><span class="sxs-lookup"><span data-stu-id="3d71b-213">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
>
> * <span data-ttu-id="3d71b-214">Развертывание ресурсов в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="3d71b-214">Deploy resources to your Azure subscription.</span></span> <span data-ttu-id="3d71b-215">Все ресурсы были настроены с помощью **бесплатного уровня.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-215">All resources were configured using the **free** tier.</span></span> <span data-ttu-id="3d71b-216">В зависимости от использования бота может потребоваться масштабировать эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3d71b-216">Depending on the usage of your bot, you may have to scale these resources.</span></span>
>
> * <span data-ttu-id="3d71b-217">Чтобы использовать вкладку Moodle без бота, пропустите [4](#4-deploy-your-microsoft-teams-app).</span><span class="sxs-lookup"><span data-stu-id="3d71b-217">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="3d71b-218">Поток информации о боте Moodle</span><span class="sxs-lookup"><span data-stu-id="3d71b-218">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="3d71b-219">Чтобы установить бот, необходимо зарегистрировать его на [платформе удостоверений Майкрософт.](https://identity.microsoft.com/Landing)</span><span class="sxs-lookup"><span data-stu-id="3d71b-219">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="3d71b-220">Это позволяет боту проверить подлинность в конечных точках Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3d71b-220">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="3d71b-221">**Регистрация бота**</span><span class="sxs-lookup"><span data-stu-id="3d71b-221">**To register your bot**</span></span>

1. <span data-ttu-id="3d71b-222">Перейдите на страницу администрирования плагинов и выберите **плагины.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-222">Go to the plugins administration page, and then select **Plugins**.</span></span> <span data-ttu-id="3d71b-223">В **Microsoft 365 интеграции** выберите **вкладку Teams Параметры.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-223">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="3d71b-224">Выберите **ссылку портала регистрации приложений** Майкрософт и вопишитесь в свой Microsoft ID.</span><span class="sxs-lookup"><span data-stu-id="3d71b-224">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="3d71b-225">Введите имя приложения, например MoodleBot, и выберите кнопку **Создать.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-225">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="3d71b-226">**Скопируйте ID приложения и** вклеите его в поле **Бот-приложение на** странице **Параметры.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-226">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="3d71b-227">Выберите **кнопку Создание нового пароля.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-227">Select the **Generate New Password** button.</span></span> <span data-ttu-id="3d71b-228">Скопируйте созданный пароль и вклейте его в поле **Пароль** для бота на странице **Параметры.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-228">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="3d71b-229">Прокрутите в нижней части формы и выберите **Сохранить изменения.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-229">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="3d71b-230">После создания имени приложения и пароля разверните бот в Azure:</span><span class="sxs-lookup"><span data-stu-id="3d71b-230">After generating your application ID and password, deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3d71b-231">Выберите **Развертывание в Azure** и заполняйте форму необходимой информацией, например кодом приложения-бота, паролем для бот-приложений и секретом Moodle **на** Teams Параметры странице.</span><span class="sxs-lookup"><span data-stu-id="3d71b-231">Select **Deploy to Azure** and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password, and the Moodle Secret on the **Teams Settings** page.</span></span> <span data-ttu-id="3d71b-232">Сведения Azure на странице **Настройка.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-232">The Azure information is on the **Setup** page.</span></span> 
> * <span data-ttu-id="3d71b-233">После завершения формы выберите почтовый ящик, чтобы согласовать условия и условия.</span><span class="sxs-lookup"><span data-stu-id="3d71b-233">After completing the form, select the checkbox to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="3d71b-234">Выберите **покупку**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-234">Select **Purchase**.</span></span> <span data-ttu-id="3d71b-235">Все ресурсы Azure развернуты на бесплатном уровне.</span><span class="sxs-lookup"><span data-stu-id="3d71b-235">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="3d71b-236">После завершения развертывания ресурсов в Azure необходимо настроить плагины Microsoft 365 Moodle с конечной точкой обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="3d71b-236">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugins with a messaging endpoint.</span></span> <span data-ttu-id="3d71b-237">Вы должны получить конечную точку от бота в Azure:</span><span class="sxs-lookup"><span data-stu-id="3d71b-237">You must get the endpoint from your bot in Azure:</span></span>

1. <span data-ttu-id="3d71b-238">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3d71b-238">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="3d71b-239">В левой области выберите группы **ресурсов** и выберите группу ресурсов, используемую или созданную при развертывании бота.</span><span class="sxs-lookup"><span data-stu-id="3d71b-239">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="3d71b-240">Выберите ресурс **WebApp Bot** из списка ресурсов в группе.</span><span class="sxs-lookup"><span data-stu-id="3d71b-240">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="3d71b-241">Скопируйте **конечную точку обмена** сообщениями из **раздела Обзор.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-241">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="3d71b-242">В Moodle откройте страницу **командной Параметры** вашего Microsoft 365 Плагины Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-242">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugins.</span></span>

1. <span data-ttu-id="3d71b-243">В поле **Bot Endpoint** вклеить URL-адрес, который вы только что скопировали, и изменить слово *сообщения* на *веб-ок.*</span><span class="sxs-lookup"><span data-stu-id="3d71b-243">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="3d71b-244">URL-адрес должен отображаться следующим образом: `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="3d71b-244">The URL must appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="3d71b-245">Выберите **Сохранить изменения.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-245">Select **Save Changes**.</span></span>

1. <span data-ttu-id="3d71b-246">После сохранения изменений  **перейдите на вкладку Team Параметры,** выберите кнопку Файл манифеста загрузки и сохраните пакет манифеста приложения на компьютере для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="3d71b-246">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="3d71b-247">4. Развертывание Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="3d71b-247">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="3d71b-248">После развертывания бота в Azure и настройки для беседы с сервером Moodle необходимо развернуть Microsoft Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="3d71b-248">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="3d71b-249">Для этого необходимо загрузить файл манифеста приложения, скачаемый с Microsoft 365 команды плагинов Moodle Параметры на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="3d71b-249">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugins Team Settings page in the previous step.</span></span>

<span data-ttu-id="3d71b-250">Перед установкой приложения необходимо убедиться, что необходимо включить внешние приложения и загрузить приложения.</span><span class="sxs-lookup"><span data-stu-id="3d71b-250">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="3d71b-251">Дополнительные сведения см. в [Microsoft 365 клиента.](../concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="3d71b-251">For more information, see [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span> 

<span data-ttu-id="3d71b-252">**Развертывание приложения**</span><span class="sxs-lookup"><span data-stu-id="3d71b-252">**To deploy your app**</span></span> 

1. <span data-ttu-id="3d71b-253">Откройте **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-253">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="3d71b-254">Выберите **значок App** в нижней левой области панели навигации.</span><span class="sxs-lookup"><span data-stu-id="3d71b-254">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="3d71b-255">Выберите **ссылку Upload приложения** из списка параметров.</span><span class="sxs-lookup"><span data-stu-id="3d71b-255">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3d71b-256">Если вы вошли в систему в качестве глобального администратора, вы должны иметь возможность загрузить приложение в каталог приложений организации, в противном случае вы можете загрузить приложение только для команды, в которой вы член.</span><span class="sxs-lookup"><span data-stu-id="3d71b-256">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="3d71b-257">Выберите `manifest.zip` пакет, который вы скачали ранее, и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-257">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="3d71b-258">Если вы не скачали пакет манифеста приложения, вы можете скачать с вкладки **Team Параметры** страницы конфигурации плагинов в Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-258">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugins configuration page in Moodle.</span></span>

<span data-ttu-id="3d71b-259">Теперь, когда у вас установлено приложение, вы можете добавить вкладку в любой канал, к который у вас есть доступ.</span><span class="sxs-lookup"><span data-stu-id="3d71b-259">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="3d71b-260">Для этого перейдите по каналу, выберите символ плюс **(➕)** и выберите приложение из списка.</span><span class="sxs-lookup"><span data-stu-id="3d71b-260">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="3d71b-261">Следуйте подсказкам, чтобы завершить добавление вкладки Курс Moodle в канал.</span><span class="sxs-lookup"><span data-stu-id="3d71b-261">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="3d71b-262">5. Разрешить автоматическое создание вкладок Moodle в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3d71b-262">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="3d71b-263">Несмотря на то, что вкладки Moodle создаются вручную в Microsoft Teams, их можно создать автоматически при создании команд из синхронизации курсов.</span><span class="sxs-lookup"><span data-stu-id="3d71b-263">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to create them automatically when teams are created from course synchronization.</span></span> <span data-ttu-id="3d71b-264">Для этого необходимо настроить ID загруженного Microsoft Teams в Moodle.</span><span class="sxs-lookup"><span data-stu-id="3d71b-264">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle.</span></span>

<span data-ttu-id="3d71b-265">**Автоматическое создание вкладок Moodle**</span><span class="sxs-lookup"><span data-stu-id="3d71b-265">**To allow automatic creation of Moodle tabs**</span></span>

1. <span data-ttu-id="3d71b-266">Откройте Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3d71b-266">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="3d71b-267">Выберите значок Apps из нижней левой области панели навигации.</span><span class="sxs-lookup"><span data-stu-id="3d71b-267">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="3d71b-268">Найдите загруженное приложение **Moodle>** выберите значок **параметров** > **ссылку копирования.**</span><span class="sxs-lookup"><span data-stu-id="3d71b-268">Locate the uploaded **Moodle app** > select the **options** icon > select **copy link**.</span></span>

1. <span data-ttu-id="3d71b-269">В текстовом редакторе вклеить скопированные материалы.</span><span class="sxs-lookup"><span data-stu-id="3d71b-269">In a text editor, paste the copied content.</span></span> <span data-ttu-id="3d71b-270">Он должен содержать URL-адрес, например ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span><span class="sxs-lookup"><span data-stu-id="3d71b-270">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="3d71b-271">Скопируйте последнюю часть URL-адреса, например , который является `00112233-4455-6677-8899-aabbccddeeff` ID Microsoft Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="3d71b-271">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="3d71b-272">В Moodle откройте **вкладку Teams Moodle** на странице конфигурации Microsoft 365 Moodle Plugins.</span><span class="sxs-lookup"><span data-stu-id="3d71b-272">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugins configuration page.</span></span>

1. <span data-ttu-id="3d71b-273">Встроите ID приложения Microsoft Teams в поле ID приложения Moodle и сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="3d71b-273">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="3d71b-274">При синхронизации курса Moodle Microsoft Teams автоматически устанавливает приложение Moodle в команде, создает вкладку Moodle в общем канале Teams и настраивает ее, чтобы содержать страницу курса для курса Moodle, с которого оно синхронизировано.</span><span class="sxs-lookup"><span data-stu-id="3d71b-274">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, creates a Moodle tab in the General channel of Teams, and configures it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="3d71b-275">Теперь вы можете начать работать с курсами Moodle непосредственно с Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3d71b-275">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="3d71b-276">Чтобы поделиться с нами любыми запросами или отзывами о функциях, посетите страницу [голосовой связи пользователя.](https://microsoftteams.uservoice.com/forums/916759-moodle)</span><span class="sxs-lookup"><span data-stu-id="3d71b-276">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="3d71b-277">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="3d71b-277">See also</span></span>

- [<span data-ttu-id="3d71b-278">Интеграция веб-приложений</span><span class="sxs-lookup"><span data-stu-id="3d71b-278">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
- [<span data-ttu-id="3d71b-279">Moodle</span><span class="sxs-lookup"><span data-stu-id="3d71b-279">Moodle</span></span>](https://moodle.org/)
- <span data-ttu-id="3d71b-280">[Документация Moodle](https://docs.moodle.org/34/en/Installing_plugins).</span><span class="sxs-lookup"><span data-stu-id="3d71b-280">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>

