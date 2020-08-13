---
title: Создание и запуск первого приложения Teams
author: heath-hamilton
description: Запустите первое приложение Microsoft Teams.
ms.openlocfilehash: 98af8d8d6d89007e36c24bd34661ec21b33cbdf1
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652167"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="109ab-103">Создание и запуск первого приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="109ab-103">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="109ab-104">Вы можете быстро приступить к разработке на платформе Microsoft Teams, быстро создав и выполнив базовое приложение.</span><span class="sxs-lookup"><span data-stu-id="109ab-104">You can jump right into developing on the Microsoft Teams platform by quickly building and running a basic app.</span></span>

> [!NOTE]
> <span data-ttu-id="109ab-105">При выполнении этих учебных курсов полезно иметь опыт работы с JavaScript (в частности, реагировать на действия).</span><span class="sxs-lookup"><span data-stu-id="109ab-105">It's helpful to have working knowledge of JavaScript (specifically React) when following these tutorials.</span></span>

## <a name="set-up-your-development-account"></a><span data-ttu-id="109ab-106">Настройка учетной записи для разработки</span><span class="sxs-lookup"><span data-stu-id="109ab-106">Set up your development account</span></span>

<span data-ttu-id="109ab-107">Чтобы создать приложения для Teams, вам потребуется учетная запись Teams, разрешающая возможность загрузки неопубликованных приложений (Эта учетная запись может уже предоставляться).</span><span class="sxs-lookup"><span data-stu-id="109ab-107">To build apps for Teams, you need a Teams account that allows sideloading (your account may already provide this).</span></span> <span data-ttu-id="109ab-108">Если это не так, зарегистрируйтесь для подписки на Microsoft 365 для разработчиков, чтобы получить тестового клиента.</span><span class="sxs-lookup"><span data-stu-id="109ab-108">If it doesn't, register for a Microsoft 365 developer subscription so you can get a test tenant.</span></span>

1. <span data-ttu-id="109ab-109">Проверьте, можно ли Загрузка неопубликованных приложения в teams:</span><span class="sxs-lookup"><span data-stu-id="109ab-109">Verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="109ab-110">В клиенте Teams выберите **приложения**.</span><span class="sxs-lookup"><span data-stu-id="109ab-110">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="109ab-111">Найдите параметр для **отправки настраиваемого приложения**.</span><span class="sxs-lookup"><span data-stu-id="109ab-111">Look for an option to **Upload a custom app**.</span></span>
1. <span data-ttu-id="109ab-112">Если у вас есть этот параметр, вы можете приступить к созданию.</span><span class="sxs-lookup"><span data-stu-id="109ab-112">If you have this option, you can start building.</span></span> <span data-ttu-id="109ab-113">Если это не так, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="109ab-113">If not, do the following:</span></span>
    1. <span data-ttu-id="109ab-114">Регистрация подписки на [Microsoft 365 для разработчиков](../doc-links/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="109ab-114">Register for a [Microsoft 365 developer subscription](../doc-links/prepare-your-o365-tenant.md).</span></span>
    1. <span data-ttu-id="109ab-115">[Включите нестандартную загрузку неопубликованных приложений](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) для тестовой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="109ab-115">[Enable custom app sideloading](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for your test account.</span></span>

## <a name="get-your-development-tools"></a><span data-ttu-id="109ab-116">Получение средств разработки</span><span class="sxs-lookup"><span data-stu-id="109ab-116">Get your development tools</span></span>

<span data-ttu-id="109ab-117">Вы можете создавать приложения Teams с помощью своих предпочтительных средств, но в этом случае вам нужно быстро приступить к работе с Visual Studio Code и набором инструментов Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="109ab-117">You can build Teams apps with your preferred tools, but here's what you need to get started quickly with Visual Studio Code and the Microsoft Teams Toolkit.</span></span>

1. <span data-ttu-id="109ab-118">Установите последнюю версию [Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="109ab-118">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span>
1. <span data-ttu-id="109ab-119">В Visual Studio Code выберите **расширения** ![ Visual Studio Toolkit View ](../doc-links/images/vs-code-extensions.png) на левой панели действий и установите **набор средств Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="109ab-119">In Visual Studio Code, select **Extensions** ![visual studio toolkit view](../doc-links/images/vs-code-extensions.png) on the left Activity Bar and install the **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="109ab-120">Установите [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="109ab-120">Install [Node.js](https://nodejs.org/en/).</span></span>

## <a name="create-an-app-project"></a><span data-ttu-id="109ab-121">Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="109ab-121">Create an app project</span></span>

<span data-ttu-id="109ab-122">Набор инструментов Microsoft Teams поможет вам настроить первый проект приложения.</span><span class="sxs-lookup"><span data-stu-id="109ab-122">The Microsoft Teams Toolkit can help you set up your first app project.</span></span>

1. <span data-ttu-id="109ab-123">В Visual Studio Code Откройте набор инструментов, выбрав значок команды</span><span class="sxs-lookup"><span data-stu-id="109ab-123">In Visual Studio Code, open the toolkit by selecting the Teams icon</span></span> ![значок рабочих групп](../doc-links/images/favicon-16x16.png) <span data-ttu-id="109ab-125">на левой панели действий.</span><span class="sxs-lookup"><span data-stu-id="109ab-125">on the left Activity Bar.</span></span>
1. <span data-ttu-id="109ab-126">Выберите **создать новое приложение Teams**.</span><span class="sxs-lookup"><span data-stu-id="109ab-126">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="109ab-127">При появлении соответствующего запроса введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="109ab-127">When prompted, enter a name for your app.</span></span> <span data-ttu-id="109ab-128">Это имя приложения по умолчанию, а также имя каталога проекта на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="109ab-128">This is the default name for your app and also the name of the project directory on your local machine.</span></span>
1. <span data-ttu-id="109ab-129">На экране **добавить возможности** выберите **вкладка** **Далее**.</span><span class="sxs-lookup"><span data-stu-id="109ab-129">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="109ab-130">Установите флажок **Личная вкладка** и нажмите кнопку **Готово** , чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="109ab-130">Check the **Personal tab** option and select **Finish** to configure your project.</span></span>

![представление "Добавление вкладок" набора инструментов](../doc-links/images/toolkit-add-tabs.PNG)

<span data-ttu-id="109ab-132">По завершении вы получите компоненты формирования шаблонов приложений для создания вкладки "Личное".</span><span class="sxs-lookup"><span data-stu-id="109ab-132">Once complete, you have the app scaffolding components for building a personal tab.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="109ab-133">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="109ab-133">Run your app</span></span>

<span data-ttu-id="109ab-134">Следуйте инструкциям `README.md` в проекте, чтобы создать, запустить и развернуть приложение в Teams.</span><span class="sxs-lookup"><span data-stu-id="109ab-134">Follow the `README.md` in your project to build, run, and deploy your app to Teams.</span></span> <span data-ttu-id="109ab-135">Как правило, эти инструкции помогут вам выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="109ab-135">In general, these instructions help you do the following:</span></span>

* <span data-ttu-id="109ab-136">Размещение приложения в `localhost` .</span><span class="sxs-lookup"><span data-stu-id="109ab-136">Host your app on `localhost`.</span></span>
* <span data-ttu-id="109ab-137">[Настройте безопасный туннель с ngrok](../doc-links/debug.md#locally-hosted) , чтобы Teams мог получить доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="109ab-137">[Set up a secure tunnel with ngrok](../doc-links/debug.md#locally-hosted) so that Teams can access your app.</span></span> <span data-ttu-id="109ab-138">(Установите [ngrok](https://ngrok.com/download).)</span><span class="sxs-lookup"><span data-stu-id="109ab-138">(Install [ngrok](https://ngrok.com/download).)</span></span>
* <span data-ttu-id="109ab-139">[Загрузка неопубликованных ваше приложение](../doc-links/apps-upload.md) в клиенте Teams, используя `Development.zip` `.publish` папку в папке.</span><span class="sxs-lookup"><span data-stu-id="109ab-139">[Sideload your app](../doc-links/apps-upload.md) in the Teams client using the `Development.zip` in the `.publish` folder.</span></span>

<span data-ttu-id="109ab-140">Когда вы Загрузка неопубликованных свое приложение, оно должно выглядеть так, как показано в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="109ab-140">Once you sideload your app, it should look like this in the Teams client.</span></span>

![Вкладка "Hello World"](../doc-links/images/tab-running.png)

## <a name="important-app-project-files"></a><span data-ttu-id="109ab-142">Важные файлы проекта приложения</span><span class="sxs-lookup"><span data-stu-id="109ab-142">Important app project files</span></span>

<span data-ttu-id="109ab-143">Если проект приложения и Настройка формирования шаблонов настроены, уделите некоторое время, чтобы ознакомиться с некоторыми ключевыми файлами, с которыми работают разработчики приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="109ab-143">With your app project and scaffolding set up, take some time to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="109ab-144">Манифест приложения ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="109ab-144">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="109ab-145">В каталоге манифест приложения размещается в качестве `.publish` отправной точки для любого проекта приложения.</span><span class="sxs-lookup"><span data-stu-id="109ab-145">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="109ab-146">Манифест определяет основные атрибуты приложения и указывает на необходимые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="109ab-146">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="109ab-147">При установке приложения Teams анализирует манифест, чтобы узнать, как визуализировать приложение в клиенте.</span><span class="sxs-lookup"><span data-stu-id="109ab-147">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

<span data-ttu-id="109ab-148">В следующих руководствах вы ознакомитесь с разделами манифеста приложения для создания вкладок персональных и маркетинговых программ.</span><span class="sxs-lookup"><span data-stu-id="109ab-148">In the following tutorials, you'll focus on the sections of the app manifest for building personal and channel tabs.</span></span>

### <a name="package-developmentzip"></a><span data-ttu-id="109ab-149">Package ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="109ab-149">Package (`Development.zip`)</span></span>

<span data-ttu-id="109ab-150">Кроме того, в `.publish` каталоге должен быть пакет приложения для [Загрузка неопубликованных вашего приложения](../../overview.md#how-can-you-share-your-teams-app) в Teams.</span><span class="sxs-lookup"><span data-stu-id="109ab-150">Also located in the `.publish` directory, you need the app package to [sideload your app](../../overview.md#how-can-you-share-your-teams-app) in Teams.</span></span> <span data-ttu-id="109ab-151">Он также используется при [публикации в каталоге приложений организации](../../overview.md#how-can-you-share-your-teams-app) или [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span><span class="sxs-lookup"><span data-stu-id="109ab-151">It's also used when [publishing to your organization's app catalog](../../overview.md#how-can-you-share-your-teams-app) or [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="109ab-152">Ниже приведены некоторые сведения о файлах пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="109ab-152">Here are some details about the app package files:</span></span>

|<span data-ttu-id="109ab-153">Имя</span><span class="sxs-lookup"><span data-stu-id="109ab-153">Name</span></span>|<span data-ttu-id="109ab-154">Тип</span><span class="sxs-lookup"><span data-stu-id="109ab-154">Type</span></span>|<span data-ttu-id="109ab-155">Size</span><span class="sxs-lookup"><span data-stu-id="109ab-155">Size</span></span>|<span data-ttu-id="109ab-156">Расположение манифеста</span><span class="sxs-lookup"><span data-stu-id="109ab-156">Manifest location</span></span>|<span data-ttu-id="109ab-157">Имя файла набора инструментов</span><span class="sxs-lookup"><span data-stu-id="109ab-157">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="109ab-158">**Манифест приложения**</span><span class="sxs-lookup"><span data-stu-id="109ab-158">**App manifest**</span></span>|`.json`| <span data-ttu-id="109ab-159">—</span><span class="sxs-lookup"><span data-stu-id="109ab-159">—</span></span> | <span data-ttu-id="109ab-160">—</span><span class="sxs-lookup"><span data-stu-id="109ab-160">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="109ab-161">**Цветовой логотип**</span><span class="sxs-lookup"><span data-stu-id="109ab-161">**Color logo**</span></span>|`.png`|<span data-ttu-id="109ab-162">192 &times; 192 пикселя</span><span class="sxs-lookup"><span data-stu-id="109ab-162">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="109ab-163">**Эмблема структуры**</span><span class="sxs-lookup"><span data-stu-id="109ab-163">**Outline logo**</span></span>|`.png`|<span data-ttu-id="109ab-164">32 &times; 32 пикселя</span><span class="sxs-lookup"><span data-stu-id="109ab-164">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

### <a name="scaffolding-src"></a><span data-ttu-id="109ab-165">Формирование шаблонов ( `src` )</span><span class="sxs-lookup"><span data-stu-id="109ab-165">Scaffolding (`src`)</span></span>

<span data-ttu-id="109ab-166">Набор средств автоматически создает формирование шаблонов в `src` каталоге на основе возможностей, добавленных во время установки.</span><span class="sxs-lookup"><span data-stu-id="109ab-166">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="109ab-167">Некоторые файлы создаются независимо от типа имеющегося приложения.</span><span class="sxs-lookup"><span data-stu-id="109ab-167">Some files are created no matter what kind of app you have, though.</span></span> <span data-ttu-id="109ab-168">Например, `App.js` файл в `src/components` каталоге важен, так как он обрабатывает инициализацию и маршрутизацию приложения.</span><span class="sxs-lookup"><span data-stu-id="109ab-168">For example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="109ab-169">Самое важное, он вызывает [пакет Microsoft Teams SDK](../doc-links/using-teams-client-sdk.md) для установления связи между приложением и Teams.</span><span class="sxs-lookup"><span data-stu-id="109ab-169">Most importantly, it calls the [Microsoft Teams SDK](../doc-links/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

<span data-ttu-id="109ab-170">Дополнительные сведения об формировании шаблонов можно узнать в руководствах по созданию вкладок персональных и маркетинговых программ.</span><span class="sxs-lookup"><span data-stu-id="109ab-170">You can learn more about scaffolding in the tutorials for creating personal and channel tabs.</span></span>

## <a name="next-step"></a><span data-ttu-id="109ab-171">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="109ab-171">Next step</span></span>

<span data-ttu-id="109ab-172">Поздравляем 🎉!</span><span class="sxs-lookup"><span data-stu-id="109ab-172">🎉 Congratulations!</span></span> <span data-ttu-id="109ab-173">У вас работает приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="109ab-173">You have a running Teams app.</span></span> <span data-ttu-id="109ab-174">Нажмите приведенную ниже кнопку, чтобы узнать, как добавить в него реальный компонент.</span><span class="sxs-lookup"><span data-stu-id="109ab-174">Select the following button to learn how to add a real-world feature to it.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="109ab-175">Создание вкладки "Личное"</span><span class="sxs-lookup"><span data-stu-id="109ab-175">Build a personal tab</span></span>](add-personal-tab.md)
