---
title: Установка Moodle LMS
description: Как установить и настроить приложение интеграции Moodle для Microsoft Teams
keywords: Teams Плагины интеграции приложений Moodle
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: d7fddad80ca08fd4ca8dee352cdcbc46e8e97dcd
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566721"
---
# <a name="install-moodle-lms"></a><span data-ttu-id="3b03f-104">Установка Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="3b03f-104">Install Moodle LMS</span></span>

<span data-ttu-id="3b03f-105">В этой статье вы узнаете, как установить Moodle LMS.</span><span class="sxs-lookup"><span data-stu-id="3b03f-105">In this article you'll learn how to install the Moodle LMS.</span></span>

> [!NOTE]
> <span data-ttu-id="3b03f-106">Чтобы помочь ИТ-администраторам легко настроить Moodle и Teams интеграцию, с открытым исходным кодом Microsoft 365 Moodle Plugins обновляется для следующих:</span><span class="sxs-lookup"><span data-stu-id="3b03f-106">To help IT admins to easily set-up Moodle and Teams integration, open-source Microsoft 365 Moodle Plugins is updated for the following:</span></span>
>
> * <span data-ttu-id="3b03f-107">Автоматическая регистрация сервера Moodle с помощью [Azure Active Directory (Azure AD).](https://azure.microsoft.com/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="3b03f-107">Auto-registration of your Moodle server with [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).</span></span>
>
> * <span data-ttu-id="3b03f-108">Развертывание бота Moodle Assistant в Azure одним щелчком мыши.</span><span class="sxs-lookup"><span data-stu-id="3b03f-108">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
>
> * <span data-ttu-id="3b03f-109">Автоматическое обеспечение команд и автоматическая синхронизация зачислений команд для всех или выбора курсов Moodle.</span><span class="sxs-lookup"><span data-stu-id="3b03f-109">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
>
> * <span data-ttu-id="3b03f-110">Автоматическая установка вкладки Moodle и помощника бота Moodle в каждую синхронизированную команду.</span><span class="sxs-lookup"><span data-stu-id="3b03f-110">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>
>
> <span data-ttu-id="3b03f-111">Чтобы узнать больше о функциональности этой интеграции, с [Microsoft Teams м.](https://education.microsoft.com/resource/3dffb3a8)</span><span class="sxs-lookup"><span data-stu-id="3b03f-111">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b03f-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3b03f-112">Prerequisites</span></span>

<span data-ttu-id="3b03f-113">Ниже приведены предпосылки для установки Moodle:</span><span class="sxs-lookup"><span data-stu-id="3b03f-113">Following are the prerequisites to install Moodle:</span></span>

* <span data-ttu-id="3b03f-114">Учетные данные администратора Moodle.</span><span class="sxs-lookup"><span data-stu-id="3b03f-114">Moodle administrator credentials.</span></span>

* <span data-ttu-id="3b03f-115">Учетные данные администратора Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b03f-115">Azure AD administrator credentials.</span></span>

* <span data-ttu-id="3b03f-116">Подписка Azure, где можно создавать новые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3b03f-116">An Azure subscription where you can create new resources.</span></span>

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="3b03f-117">1. Установите Microsoft 365 Moodle Plugins</span><span class="sxs-lookup"><span data-stu-id="3b03f-117">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="3b03f-118">Интеграция Moodle в Microsoft Teams работает на открытом Microsoft 365 [комплекте плагинов Moodle.](https://github.com/Microsoft/o365-moodle)</span><span class="sxs-lookup"><span data-stu-id="3b03f-118">Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugins set](https://github.com/Microsoft/o365-moodle).</span></span>

### <a name="requisite-applications-and-plugins"></a><span data-ttu-id="3b03f-119">Необходимые приложения и плагины</span><span class="sxs-lookup"><span data-stu-id="3b03f-119">Requisite applications and plugins</span></span>

<span data-ttu-id="3b03f-120">Убедитесь в том, чтобы установить и скачать следующее, прежде чем приступить к Microsoft 365 установки плагинов Moodle:</span><span class="sxs-lookup"><span data-stu-id="3b03f-120">Ensure to install and download the following before proceeding with the Microsoft 365 Moodle plugins installation:</span></span>

1. <span data-ttu-id="3b03f-121">Убедитесь в установке [текущей стабильной версии Moodle](https://download.moodle.org/releases/latest/).</span><span class="sxs-lookup"><span data-stu-id="3b03f-121">Ensure to install a [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="3b03f-122">Загрузите и сохраните плагины Moodle [OpenID Подключение](https://moodle.org/plugins/auth_oidc) и [Microsoft 365 интеграции](https://moodle.org/plugins/local_o365) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3b03f-122">Download and save the Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins to your local computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3b03f-123">Для интеграции Подключение Microsoft 365 openID и Teams интеграции.</span><span class="sxs-lookup"><span data-stu-id="3b03f-123">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span>
    >
    > <span data-ttu-id="3b03f-124">Кроме того, [Microsoft 365 Teams theme](https://moodle.org/plugins/theme_boost_o365teams) плагины настоятельно рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="3b03f-124">In addition, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugins is highly recommended.</span></span>

### <a name="microsoft-365-moodle-plugins"></a><span data-ttu-id="3b03f-125">Microsoft 365 Плагины Moodle</span><span class="sxs-lookup"><span data-stu-id="3b03f-125">Microsoft 365 Moodle plugins</span></span>

1. <span data-ttu-id="3b03f-126">Войтите на сервер Moodle в качестве администратора и выберите **администрирование** [сайта из Параметры, расположенного](https://docs.moodle.org/22/en/Settings_block) в левой навигационной панели.</span><span class="sxs-lookup"><span data-stu-id="3b03f-126">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="3b03f-127">Выберите **вкладку Plugins,** а затем **выберите Установить плагины**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-127">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="3b03f-128">Из **плагинов Install из раздела файла qIP** **выберите файл.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-128">From the **Install plugins from ZIP file** section, select **Choose a file**.</span></span>

1. <span data-ttu-id="3b03f-129">Выберите **Upload файл с** левой навигационной панели, просмотрите файл, который вы скачали, и **выберите Upload этом файле.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-129">Select **Upload a file** option from the left navigation panel, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="3b03f-130">Выберите **администрирование** сайта с левой навигационной панели, чтобы вернуться к панели мониторинга администратора.</span><span class="sxs-lookup"><span data-stu-id="3b03f-130">Select **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="3b03f-131">Прокрутите вниз к **локальным плагинам** и выберите **Microsoft 365 интеграции.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-131">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span>

    > [!IMPORTANT]
    >
    > * <span data-ttu-id="3b03f-132">Держите ваш Microsoft 365 Moodle Plugins страницу конфигурации открытым в отдельной вкладке браузера, как вам нужно вернуться к этому набору страниц на протяжении всего процесса.</span><span class="sxs-lookup"><span data-stu-id="3b03f-132">Keep your Microsoft 365 Moodle Plugins configuration page open in a separate browser tab as you need to return to this set of pages throughout the process.</span></span>  
    >
    > * <span data-ttu-id="3b03f-133">Если у вас нет существующего сайта Moodle, перейдите в [Репо Moodle на Azure](https://github.com/azure/moodle) и быстро разверните экземпляр Moodle и настройите его под свои потребности.</span><span class="sxs-lookup"><span data-stu-id="3b03f-133">If you do not have an existing Moodle site, go to the [Moodle on Azure](https://github.com/azure/moodle) repo, and quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a><span data-ttu-id="3b03f-134">2. Настройте соединение между Microsoft 365 и Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="3b03f-134">2. Configure the connection between the Microsoft 365 plugins and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="3b03f-135">Необходимо настроить соединение между Microsoft 365 и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b03f-135">You must configure the connection between the Microsoft 365 plugins and Azure AD.</span></span>

### <a name="requisites"></a><span data-ttu-id="3b03f-136">вооружение</span><span class="sxs-lookup"><span data-stu-id="3b03f-136">Requisites</span></span>

<span data-ttu-id="3b03f-137">Зарегистрируйте Moodle в качестве приложения в Azure AD, используя скрипт PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b03f-137">Register Moodle as an application in your Azure AD, using the PowerShell script.</span></span> <span data-ttu-id="3b03f-138">Скрипт Powershell предусматривает следующее:</span><span class="sxs-lookup"><span data-stu-id="3b03f-138">The Powershell script provisions the following:</span></span>

* <span data-ttu-id="3b03f-139">Новое приложение Azure AD для Microsoft 365, которое используется службой Microsoft 365 Moodle Plugins.</span><span class="sxs-lookup"><span data-stu-id="3b03f-139">A new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugins.</span></span>
* <span data-ttu-id="3b03f-140">Приложение для вашего Microsoft 365, настроить необходимые URL-адреса ответов и разрешения для готового приложения, и возвращает `AppID` и `Key` .</span><span class="sxs-lookup"><span data-stu-id="3b03f-140">The app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and returns the `AppID` and `Key`.</span></span>

<span data-ttu-id="3b03f-141">Используйте `AppID` сгенерированную `Key` и в Microsoft 365 страницу настройки Moodle Plugins для настройки вашего сайта сервера Moodle с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b03f-141">Use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugins setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="3b03f-142">Скрипт PowerShell не обновляется с последними элементами конфигурации, поэтому вы должны завершить конфигурацию вручную, следуя шагам, изложенным в страницах Moodle [3.8.0.4 и 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) [и 3.8.0.5 и 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release)</span><span class="sxs-lookup"><span data-stu-id="3b03f-142">The PowerShell script is not updated with the latest configuration items, therefore, you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span>
>
> * <span data-ttu-id="3b03f-143">Для получения дополнительной информации о регистрации экземпляра Moodle вручную, [см.](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)</span><span class="sxs-lookup"><span data-stu-id="3b03f-143">For more information on registering your Moodle instance manually, see [Register your Moodle instance as an application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="3b03f-144">Вкладка Moodle для Microsoft Teams потока</span><span class="sxs-lookup"><span data-stu-id="3b03f-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="3b03f-145">Со страницы плагинов Microsoft 365 интеграции выберите вкладку **Setup.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-145">From the Microsoft 365 Integration plugins page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="3b03f-146">Выберите **кнопку «Скачать powerShell Script»** и сохраните ее в качестве папки с почтовым индексом на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3b03f-146">Select the **Download PowerShell Script** button and save it as a ZIP folder to your local computer.</span></span>

1. <span data-ttu-id="3b03f-147">Подготовь скрипт PowerShell из файла ЗИП следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3b03f-147">Prepare the PowerShell script from the ZIP file as follows:</span></span> 

    1. <span data-ttu-id="3b03f-148">Скачать и извлечь `Moodle-AzureAD-Powershell.zip` файл.</span><span class="sxs-lookup"><span data-stu-id="3b03f-148">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="3b03f-149">Откройте извлеченную папку.</span><span class="sxs-lookup"><span data-stu-id="3b03f-149">Open the extracted folder.</span></span>
    1. <span data-ttu-id="3b03f-150">Нажмите правой `Moodle-AzureAD-Script.ps1` кнопкой мыши на файл и **выберите Свойства**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-150">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="3b03f-151">Под общей **вкладкой** окна Свойства выберите флажок `Unblock` рядом с **атрибутом безопасности,** расположенным в нижней части окна.</span><span class="sxs-lookup"><span data-stu-id="3b03f-151">Under the **General** tab of the Properties window, select the `Unblock` checkbox next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="3b03f-152">Нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-152">Select **OK**.</span></span>
    1. <span data-ttu-id="3b03f-153">Скопируйте путь каталога к извлеченной папке.</span><span class="sxs-lookup"><span data-stu-id="3b03f-153">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="3b03f-154">Вы запустите PowerShell в качестве администратора:</span><span class="sxs-lookup"><span data-stu-id="3b03f-154">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="3b03f-155">Выберите «Начать».</span><span class="sxs-lookup"><span data-stu-id="3b03f-155">Select Start.</span></span>
    1. <span data-ttu-id="3b03f-156">Тип PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b03f-156">Type PowerShell.</span></span>
    1. <span data-ttu-id="3b03f-157">Нажмите правой кнопкой **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-157">Right-click on **Windows PowerShell**.</span></span>
    1. <span data-ttu-id="3b03f-158">Выберите **Run в качестве администратора**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-158">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="3b03f-159">Перейдите в неразметимый каталог, `cd .../.../Moodle-AzureAD-Powershell` `.../...` введя, где находится путь к каталогу.</span><span class="sxs-lookup"><span data-stu-id="3b03f-159">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="3b03f-160">Выполнить скрипт PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3b03f-160">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="3b03f-161">Введите `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .</span><span class="sxs-lookup"><span data-stu-id="3b03f-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="3b03f-162">Введите `./Moodle-AzureAD-Script.ps1` .</span><span class="sxs-lookup"><span data-stu-id="3b03f-162">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="3b03f-163">Вопишитесь на Microsoft 365 учетную запись администратора во всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="3b03f-163">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="3b03f-164">Введите название приложения Azure AD, например, плагинов Moodle или Moodle.</span><span class="sxs-lookup"><span data-stu-id="3b03f-164">Enter the name of the Azure AD Application, for example, Moodle or Moodle plugins.</span></span>
    1. <span data-ttu-id="3b03f-165">Введите URL-адрес сервера Moodle.</span><span class="sxs-lookup"><span data-stu-id="3b03f-165">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="3b03f-166">Копировать **идентификатор приложения `AppID` () и** ключ приложения **`Key` () порожденный** скриптом и сохранить их.</span><span class="sxs-lookup"><span data-stu-id="3b03f-166">Copy the **Application ID (`AppID`)** and **Application Key(`Key`)** generated by the script and save them.</span></span>

1. <span data-ttu-id="3b03f-167">Далее вы должны `AppID` добавить и в Microsoft 365 `Key` Moodle Plugins.</span><span class="sxs-lookup"><span data-stu-id="3b03f-167">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugins.</span></span> <span data-ttu-id="3b03f-168">Вернитесь на страницу администрирования плагинов, администрация сайта > плагины > Microsoft 365 интеграции.</span><span class="sxs-lookup"><span data-stu-id="3b03f-168">Return to the plugins administration page, Site administration > Plugins > Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="3b03f-169">На **вкладке Настройка** добавить и `AppID` вы `Key` скопировали ранее, а затем выбрать **сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-169">On the **Setup** tab add the `AppID` and `Key` you copied previously, and then select **Save changes**.</span></span> <span data-ttu-id="3b03f-170">После обновления страницы можно увидеть новый раздел **Выберите метод подключения.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-170">After the page refreshes, you can see a new section **Choose connection method**.</span></span>

1. <span data-ttu-id="3b03f-171">В **методе «Выбрать соединение»** выберите флажок с пометкой **«По умолчанию»,** а затем снова **выберите изменения «Сохранить».**</span><span class="sxs-lookup"><span data-stu-id="3b03f-171">In the **Choose connection method**, select the checkbox labeled **Default**, and then select **Save changes** again.</span></span>

1. <span data-ttu-id="3b03f-172">После обновления страницы вы можете увидеть еще один новый раздел Администратор **согласие & дополнительной информации**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-172">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="3b03f-173">Выберите **ссылку «Предоставить** согласие администратора», введите Microsoft 365 учетных данных Глобального администратора, **а** затем примите разрешение на предоставление разрешений.</span><span class="sxs-lookup"><span data-stu-id="3b03f-173">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="3b03f-174">Рядом с полем **Арендатор Azure AD** выберите **кнопку Обнаружения.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-174">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="3b03f-175">Рядом с **OneDrive для бизнеса URL,** выберите **кнопку Обнаружения.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-175">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="3b03f-176">После заполнения полей снова выберите **кнопку сохранения** изменений.</span><span class="sxs-lookup"><span data-stu-id="3b03f-176">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="3b03f-177">Выберите **кнопку** Обновления для проверки установки, а затем выберите **сохранить изменения.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-177">Select the **Update** button to verify the installation, and then select **Save changes**.</span></span>

1. <span data-ttu-id="3b03f-178">Синхронизация пользователей между сервером Moodle и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b03f-178">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="3b03f-179">Для начала сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3b03f-179">To get started:</span></span>

    > [!NOTE]
    > <span data-ttu-id="3b03f-180">В зависимости от среды, вы можете выбрать различные варианты на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="3b03f-180">Depending on your environment, you can select different options during this stage.</span></span>

1. <span data-ttu-id="3b03f-181">Синхронизация пользователей между сервером Moodle и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b03f-181">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="3b03f-182">В зависимости от среды, вы можете выбрать различные варианты на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="3b03f-182">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="3b03f-183">Для начала сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3b03f-183">To get started:</span></span>
    1. <span data-ttu-id="3b03f-184">Переключитесь **на вкладку Параметры синхронизации.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-184">Switch to the **Sync Settings tab**.</span></span>

    1. <span data-ttu-id="3b03f-185">В разделе **Синхронизация пользователей с разделом Azure AD** выберите флажки, применимые к вашей среде.</span><span class="sxs-lookup"><span data-stu-id="3b03f-185">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="3b03f-186">Вы должны выбрать следующее:</span><span class="sxs-lookup"><span data-stu-id="3b03f-186">You must select the following:</span></span>  

        <span data-ttu-id="3b03f-187">✔ создать учетные записи в Moodle для пользователей в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b03f-187">✔ Create accounts in Moodle for users in Azure AD.</span></span>

        <span data-ttu-id="3b03f-188">✔ все учетные записи в Moodle для пользователей в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b03f-188">✔ Update all accounts in Moodle for users in Azure AD.</span></span>

    1. <span data-ttu-id="3b03f-189">В разделе **Ограничение создания пользователей** можно настроить фильтр для ограничения пользователей Azure AD, синхронизированных с Moodle.</span><span class="sxs-lookup"><span data-stu-id="3b03f-189">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="3b03f-190">Раздел **Отображение поля** пользователя позволяет настроить Azure AD для отображения поля профиля пользователя Moodle.</span><span class="sxs-lookup"><span data-stu-id="3b03f-190">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="3b03f-191">В **разделе Teams Sync** можно выбрать автоматически создавать группы, такие как команды для некоторых или всех существующих курсов Moodle.</span><span class="sxs-lookup"><span data-stu-id="3b03f-191">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

13. <span data-ttu-id="3b03f-192">Для [проверки заданий cron](https://docs.moodle.org/310/en/Cron) и запуска их вручную для первого запуска выберите **ссылку на страницу управления запланированными** **задачами в разделе Sync с разделом Azure AD.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-192">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="3b03f-193">Это ведет вас на страницу **запланированных** задач.</span><span class="sxs-lookup"><span data-stu-id="3b03f-193">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="3b03f-194">Прокрутите вниз и найдите **пользователей Sync с помощью задания Azure AD** и выберите **Run now.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-194">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="3b03f-195">Если вы выберете для создания групп на основе существующих курсов, вы также можете **запустить группы пользователей Создать в Microsoft 365** работе.</span><span class="sxs-lookup"><span data-stu-id="3b03f-195">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="3b03f-196">Moodle [Cron работает в](https://docs.moodle.org/310/en/Cron) соответствии с графиком задач.</span><span class="sxs-lookup"><span data-stu-id="3b03f-196">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="3b03f-197">Расписание по умолчанию один раз в день.</span><span class="sxs-lookup"><span data-stu-id="3b03f-197">The default schedule is once a day.</span></span> <span data-ttu-id="3b03f-198">Тем не менее, cron должен работать чаще, чтобы держать все в синхронизации.</span><span class="sxs-lookup"><span data-stu-id="3b03f-198">However, the cron must run more frequently to keep everything in sync.</span></span>

1. <span data-ttu-id="3b03f-199">Вернитесь на страницу администрирования **плагинов, администрация сайта > плагины > Microsoft 365 интеграции** и **выберите Teams Параметры страницу.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-199">Return to the plugins administration page, **Site administration > Plugins > Microsoft 365 Integration**, and select the **Teams Settings** page.</span></span>

1. <span data-ttu-id="3b03f-200">На **Teams Параметры** настройке необходимых настроек для интеграции Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="3b03f-200">On the **Teams Settings** page, configure the required settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="3b03f-201">Для включения **OpenID Подключение,** выберите **ссылку «Управлять аутентификацией»** и выберите **значок глаза на линии OpenId Подключение,** если она вытеха.</span><span class="sxs-lookup"><span data-stu-id="3b03f-201">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="3b03f-202">Для включения встраивания кадров выберите **ссылку http Security,** а затем выберите флажок рядом **с встраиванием кадра.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-202">To enable frame embedding, select the **HTTP Security** link, and then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="3b03f-203">Для включения веб-сервисов, позволяющих использовать функции Moodle API, выберите **ссылку Расширенные функции,** а затем убедитесь, что флажок **рядом с веб-службами Enable** выбран.</span><span class="sxs-lookup"><span data-stu-id="3b03f-203">To enable web services, which enables the Moodle API features, select the **Advanced Features** link, and then ensure the checkbox next to **Enable web services** is selected.</span></span>
    1. <span data-ttu-id="3b03f-204">Для включения внешних служб для Microsoft 365, выберите **ссылку Внешних** служб, а затем:</span><span class="sxs-lookup"><span data-stu-id="3b03f-204">To enable the external services for Microsoft 365, select the **External services** link, and then:</span></span>  

        <span data-ttu-id="3b03f-205">✔ **выберите редактировать** **строку Microsoft 365-сервисов Moodle.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-205">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>

        <span data-ttu-id="3b03f-206">✔ выберите флажок рядом с **Enabled,** а затем выберите **Сохранить изменения**</span><span class="sxs-lookup"><span data-stu-id="3b03f-206">✔ Select the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="3b03f-207">Отредактировать ваши подлинные разрешения пользователей, чтобы позволить им создавать токены веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3b03f-207">Edit your authenticated user permissions to allow them to create web service tokens.</span></span>

        <span data-ttu-id="3b03f-208">✔ выберите редактирование **роли Аутентифицированная ссылка** пользователя.</span><span class="sxs-lookup"><span data-stu-id="3b03f-208">✔ Select the **Editing role Authenticated user** link.</span></span>

        <span data-ttu-id="3b03f-209">✔ Прокрутите вниз и найдите **возможность токена Create a web service** и выберите **флажок Allow.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-209">✔ Scroll down and find the **Create a web service token** capability and select the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="3b03f-210">3. Развертывание помощника Бота Moodle в Azure</span><span class="sxs-lookup"><span data-stu-id="3b03f-210">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="3b03f-211">Бесплатный помощник Мудл бот для Microsoft Teams помогает учителям и студентам ответить на вопросы о своих курсах, заданиях, классах и другой информации в Moodle.</span><span class="sxs-lookup"><span data-stu-id="3b03f-211">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades, and other information in Moodle.</span></span> <span data-ttu-id="3b03f-212">Бот также отправляет уведомления Moodle студентам и преподавателям в течение Teams.</span><span class="sxs-lookup"><span data-stu-id="3b03f-212">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="3b03f-213">Бот является проектом с открытым исходным кодом, поддерживаемым корпорацией Майкрософт, и доступен [на GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span><span class="sxs-lookup"><span data-stu-id="3b03f-213">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
>
> * <span data-ttu-id="3b03f-214">Развертывание ресурсов в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="3b03f-214">Deploy resources to your Azure subscription.</span></span> <span data-ttu-id="3b03f-215">Все ресурсы были настроены с использованием **свободного** уровня.</span><span class="sxs-lookup"><span data-stu-id="3b03f-215">All resources were configured using the **free** tier.</span></span> <span data-ttu-id="3b03f-216">В зависимости от использования бота, возможно, придется масштабировать эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3b03f-216">Depending on the usage of your bot, you may have to scale these resources.</span></span>
>
> * <span data-ttu-id="3b03f-217">Чтобы использовать вкладку Moodle без бота, перейти к [4](#4-deploy-your-microsoft-teams-app).</span><span class="sxs-lookup"><span data-stu-id="3b03f-217">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="3b03f-218">Поток информации о боте Moodle</span><span class="sxs-lookup"><span data-stu-id="3b03f-218">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="3b03f-219">Чтобы установить бота, необходимо зарегистрировать его на платформе [Microsoft Identity Platform.](https://identity.microsoft.com/Landing)</span><span class="sxs-lookup"><span data-stu-id="3b03f-219">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="3b03f-220">Это позволяет вашему боту проверить подлинность конечных точек Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3b03f-220">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="3b03f-221">**Регистрация бота**</span><span class="sxs-lookup"><span data-stu-id="3b03f-221">**To register your bot**</span></span>

1. <span data-ttu-id="3b03f-222">Перейдите на страницу администрирования плагинов, а затем **выберите Plugins**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-222">Go to the plugins administration page, and then select **Plugins**.</span></span> <span data-ttu-id="3b03f-223">В **Microsoft 365 интеграции** выберите **Teams Параметры вкладку.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-223">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="3b03f-224">Выберите **ссылку на Портал регистрации приложений** Майкрософт и вопишитесь на идентификатор Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3b03f-224">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="3b03f-225">Введите имя для приложения, например MoodleBot, и выберите **кнопку «Создать».**</span><span class="sxs-lookup"><span data-stu-id="3b03f-225">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="3b03f-226">**Скопируйте идентификатор приложения** и вставьте его в поле **идентификации приложений** Bot **на странице Параметры** команды.</span><span class="sxs-lookup"><span data-stu-id="3b03f-226">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="3b03f-227">Выберите **кнопку «Создать новый** пароль».</span><span class="sxs-lookup"><span data-stu-id="3b03f-227">Select the **Generate New Password** button.</span></span> <span data-ttu-id="3b03f-228">Скопируйте сгенерированный пароль и вставьте **его в поле Bot Application Password** на странице **Параметры** команды.</span><span class="sxs-lookup"><span data-stu-id="3b03f-228">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="3b03f-229">Прокрутите в нижней части формы и выберите **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-229">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="3b03f-230">После создания идентификатора приложения и пароля разверните бота в Azure:</span><span class="sxs-lookup"><span data-stu-id="3b03f-230">After generating your application ID and password, deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3b03f-231">Выберите **Развертывание в Azure** и заполномоть форму необходимой информацией, такой как идентификатор приложения Bot, пароль приложения Bot и секрет Moodle на **Teams Параметры** странице.</span><span class="sxs-lookup"><span data-stu-id="3b03f-231">Select **Deploy to Azure** and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password, and the Moodle Secret on the **Teams Settings** page.</span></span> <span data-ttu-id="3b03f-232">Информация Azure находится на странице **Настройки.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-232">The Azure information is on the **Setup** page.</span></span> 
> * <span data-ttu-id="3b03f-233">После заполнения формы выберите флажок, чтобы согласовать условия.</span><span class="sxs-lookup"><span data-stu-id="3b03f-233">After completing the form, select the checkbox to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="3b03f-234">Выберите **Покупка**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-234">Select **Purchase**.</span></span> <span data-ttu-id="3b03f-235">Все ресурсы Azure развернуты на свободном уровне.</span><span class="sxs-lookup"><span data-stu-id="3b03f-235">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="3b03f-236">После завершения развертывания ресурсов в Azure необходимо настроить плагины Microsoft 365 Moodle с конечной точкой обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="3b03f-236">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugins with a messaging endpoint.</span></span> <span data-ttu-id="3b03f-237">Вы должны получить конечную точку от вашего бота в Azure:</span><span class="sxs-lookup"><span data-stu-id="3b03f-237">You must get the endpoint from your bot in Azure:</span></span>

1. <span data-ttu-id="3b03f-238">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b03f-238">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="3b03f-239">В левом стекле выберите группы **ресурсов и** выберите группу ресурсов, которую вы использовали или создали, развертывая бота.</span><span class="sxs-lookup"><span data-stu-id="3b03f-239">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="3b03f-240">Выберите **ресурс WebApp Bot** из списка ресурсов группы.</span><span class="sxs-lookup"><span data-stu-id="3b03f-240">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="3b03f-241">Копировать **конечную точку обмена** сообщениями из **раздела** Обзор.</span><span class="sxs-lookup"><span data-stu-id="3b03f-241">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="3b03f-242">В Moodle откройте **страницу команды Параметры** вашего веб-Microsoft 365 Moodle Plugins.</span><span class="sxs-lookup"><span data-stu-id="3b03f-242">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugins.</span></span>

1. <span data-ttu-id="3b03f-243">В поле **Bot Endpoint вставьте** URL-адрес, который вы только что скопировали, и измените *слово сообщения* *на webhook*.</span><span class="sxs-lookup"><span data-stu-id="3b03f-243">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="3b03f-244">URL-адрес должен отображаться следующим образом: `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="3b03f-244">The URL must appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="3b03f-245">Выберите **Сохранить Изменения**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-245">Select **Save Changes**.</span></span>

1. <span data-ttu-id="3b03f-246">После сохранения изменений вернитесь во **вкладку Team Параметры,** выберите **кнопку файла Download manifest** и сохраните пакет манифестов приложения на компьютере для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="3b03f-246">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="3b03f-247">4. Развертывание Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="3b03f-247">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="3b03f-248">После развертывания бота в Azure и настройки для можно поговорить с сервером Moodle, необходимо развернуть Microsoft Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="3b03f-248">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="3b03f-249">Для этого необходимо загрузить файл манифеста приложения, который вы скачали с Microsoft 365 Moodle Plugins Team Параметры на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="3b03f-249">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugins Team Settings page in the previous step.</span></span>

<span data-ttu-id="3b03f-250">Перед установкой приложения необходимо обеспечить возможность включения внешних приложений и загрузки приложений.</span><span class="sxs-lookup"><span data-stu-id="3b03f-250">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="3b03f-251">Для получения дополнительной информации с [Microsoft 365 м.](../concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="3b03f-251">For more information, see [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span> 

<span data-ttu-id="3b03f-252">**Развертывание приложения**</span><span class="sxs-lookup"><span data-stu-id="3b03f-252">**To deploy your app**</span></span> 

1. <span data-ttu-id="3b03f-253">Открытый **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-253">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="3b03f-254">Выберите **значок** Приложения в левом нижнем левом районе навигационного бара.</span><span class="sxs-lookup"><span data-stu-id="3b03f-254">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="3b03f-255">Выберите **Upload ссылку на пользовательское** приложение из списка опций.</span><span class="sxs-lookup"><span data-stu-id="3b03f-255">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3b03f-256">Если вы вошли в систему в качестве глобального администратора, вы должны иметь возможность загрузить приложение в каталог приложений вашей организации, в противном случае вы можете загрузить приложение только для команды, в которой вы находитесь.</span><span class="sxs-lookup"><span data-stu-id="3b03f-256">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="3b03f-257">Выберите `manifest.zip` пакет, который вы скачали ранее, и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3b03f-257">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="3b03f-258">Если вы еще не скачали пакет манифестов приложения, вы можете **скачать Параметры** вкладке страницы конфигурации плагинов в Moodle.</span><span class="sxs-lookup"><span data-stu-id="3b03f-258">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugins configuration page in Moodle.</span></span>

<span data-ttu-id="3b03f-259">Теперь, когда приложение установлено, вы можете добавить вкладку к любому каналу, к который у вас есть доступ.</span><span class="sxs-lookup"><span data-stu-id="3b03f-259">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="3b03f-260">Для этого перейдите на канал, выберите **символ плюс** (➕) и выберите приложение из списка.</span><span class="sxs-lookup"><span data-stu-id="3b03f-260">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="3b03f-261">Следуйте подсказкам, чтобы закончить добавление вкладки курса Moodle к каналу.</span><span class="sxs-lookup"><span data-stu-id="3b03f-261">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="3b03f-262">5. Разрешить автоматическое создание вкладок Moodle в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3b03f-262">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="3b03f-263">Хотя вкладки Moodle создаются вручную в Microsoft Teams, вы можете решить создать их автоматически, когда команды создаются из синхронизации курса.</span><span class="sxs-lookup"><span data-stu-id="3b03f-263">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to create them automatically when teams are created from course synchronization.</span></span> <span data-ttu-id="3b03f-264">Для этого необходимо настроить идентификатор загруженного приложения Microsoft Teams Moodle.</span><span class="sxs-lookup"><span data-stu-id="3b03f-264">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle.</span></span>

<span data-ttu-id="3b03f-265">**Автоматическое создание вкладок Moodle**</span><span class="sxs-lookup"><span data-stu-id="3b03f-265">**To allow automatic creation of Moodle tabs**</span></span>

1. <span data-ttu-id="3b03f-266">Откройте Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3b03f-266">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="3b03f-267">Выберите значок Apps из нижнего левого региона навигационного бара.</span><span class="sxs-lookup"><span data-stu-id="3b03f-267">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="3b03f-268">Найдите загруженное приложение **Moodle** > выберите значок **опций** > выберите **ссылку на копию.**</span><span class="sxs-lookup"><span data-stu-id="3b03f-268">Locate the uploaded **Moodle app** > select the **options** icon > select **copy link**.</span></span>

1. <span data-ttu-id="3b03f-269">В текстовом редакторе вставьте скопированный контент.</span><span class="sxs-lookup"><span data-stu-id="3b03f-269">In a text editor, paste the copied content.</span></span> <span data-ttu-id="3b03f-270">Он должен содержать URL-адрес, такой как ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span><span class="sxs-lookup"><span data-stu-id="3b03f-270">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="3b03f-271">Копировать последнюю часть URL, `00112233-4455-6677-8899-aabbccddeeff` например, , который является идентификатором Microsoft Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="3b03f-271">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="3b03f-272">В Moodle откройте **вкладку приложения Teams Moodle** со страницы конфигурации Microsoft 365 Moodle Plugins.</span><span class="sxs-lookup"><span data-stu-id="3b03f-272">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugins configuration page.</span></span>

1. <span data-ttu-id="3b03f-273">Вставьте идентификатор приложения Microsoft Teams поле идентификатора приложения Moodle и сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="3b03f-273">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="3b03f-274">Когда курс Moodle синхронизируется, Microsoft Teams автоматически устанавливает приложение Moodle в команде, создает вкладку Moodle в общем канале Teams и настраивает ее, чтобы содержать страницу курса для курса Moodle, с которой он синхронизируется.</span><span class="sxs-lookup"><span data-stu-id="3b03f-274">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, creates a Moodle tab in the General channel of Teams, and configures it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="3b03f-275">Теперь вы можете начать работать с курсами Moodle непосредственно с Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3b03f-275">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="3b03f-276">Чтобы поделиться с нами любыми запросами на функции или отзывами, посетите нашу [страницу Голос пользователя.](https://microsoftteams.uservoice.com/forums/916759-moodle)</span><span class="sxs-lookup"><span data-stu-id="3b03f-276">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="3b03f-277">См. также</span><span class="sxs-lookup"><span data-stu-id="3b03f-277">See also</span></span>

- [<span data-ttu-id="3b03f-278">Интеграция веб-приложений</span><span class="sxs-lookup"><span data-stu-id="3b03f-278">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
- [<span data-ttu-id="3b03f-279">Мудл</span><span class="sxs-lookup"><span data-stu-id="3b03f-279">Moodle</span></span>](https://moodle.org/)
- <span data-ttu-id="3b03f-280">[Документация Moodle](https://docs.moodle.org/34/en/Installing_plugins).</span><span class="sxs-lookup"><span data-stu-id="3b03f-280">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>

