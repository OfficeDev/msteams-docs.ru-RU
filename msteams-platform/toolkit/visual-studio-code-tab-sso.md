---
title: Проверка подлинности с помощью единого набор средств и Visual Studio для вкладок
description: Создайте вкладку, которая поддерживает вход с одним входом и вызовы Microsoft Graph непосредственно в Visual Studio с помощью microsoft Teams набор средств
keywords: команды visual studio code toolkit tabs sso graph authentication Azure identity platform
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: daf9a1b0bb64fee9584d0f58d749cf2b1ccaa4ef
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018427"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="4cd1c-104">Проверка подлинности с помощью единого набор средств и Visual Studio для вкладок</span><span class="sxs-lookup"><span data-stu-id="4cd1c-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="4cd1c-105">Программа Microsoft Teams набор средств позволяет создавать проверку подлинности для приложений-вкладок непосредственно в Visual Studio коде.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="4cd1c-106">Набор инструментов поможет вам в этом процессе и предоставляет все необходимое, включая подготовка регистрации платформы удостоверений Майкрософт на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="4cd1c-107">Начало работы — создание проекта</span><span class="sxs-lookup"><span data-stu-id="4cd1c-107">Get started — create a project</span></span>

1. <span data-ttu-id="4cd1c-108">Создание нового проекта в наборе инструментов.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="4cd1c-109">Выберите вкладку в качестве типа расширения, который вы хотите создать.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="4cd1c-110">Выберите параметр для поддержки SSO.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="4cd1c-111">После установки в панели действий набор средств Teams Visual Studio коде.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="4cd1c-112">Если нет, щелкните правой кнопкой мыши в панели действий и выберите **Microsoft Teams,** чтобы закрепить набор инструментов для легкого доступа.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="4cd1c-113">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="4cd1c-113">Configure your project</span></span>

1. <span data-ttu-id="4cd1c-114">Чтобы включить SSO в Teams, ваше приложение должно иметь ресурс регистрации приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="4cd1c-115">В набор средств teams будет предусмотрена регистрация приложения от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="4cd1c-116">Введите URL-адрес, в котором будет организовано ваше приложение, и выберите **следующий**.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="4cd1c-117">Регистрация приложения будет настроена с помощью предоставленного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="4cd1c-118">Сведения о конфигурации приложения будут храниться в файлах в `.env` исходных кодах проекта.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="4cd1c-119">Если вы хотите узнать больше о подготовке регистрации приложения  Azure, см. в нашей единой поддержке документации по вкладке. [](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="4cd1c-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="4cd1c-120">Вам потребуется перейти к **azure App Registrations** и обновить *URI API* и перенаправить *URL-адреса* всякий раз, когда вы измените этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="4cd1c-121">Запуск проекта</span><span class="sxs-lookup"><span data-stu-id="4cd1c-121">Run your project</span></span>

1. <span data-ttu-id="4cd1c-122">Выберите **установку npm** из `api-server` папки.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="4cd1c-123">Затем **запустите npm.**</span><span class="sxs-lookup"><span data-stu-id="4cd1c-123">Then **npm start**.</span></span>
1. <span data-ttu-id="4cd1c-124">Выберите **установку npm** из `.src` папки.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="4cd1c-125">Затем **запустите npm.**</span><span class="sxs-lookup"><span data-stu-id="4cd1c-125">Then **npm start**.</span></span>
1. <span data-ttu-id="4cd1c-126">Если вы используете службу тоннелей, например [ngrok,](https://ngrok.com/)запустите ее и убедитесь, что URL-адрес совпадает с тем, что вы ввели в мастер создания проекта.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="4cd1c-127">Если этого не сделать, необходимо обновить _URI API_ и перенаправить _URL-адрес_ в регистрации приложений, созданной в Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="4cd1c-128">Перейдите к панели действий в левой части окна Visual Studio кода.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="4cd1c-129">Выберите **значок Выполнить,** чтобы отобразить представление **Run и Debug.**</span><span class="sxs-lookup"><span data-stu-id="4cd1c-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="4cd1c-130">Вы также можете использовать ярлык клавиатуры **Ctrl+Shift+D**.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="4cd1c-131">Вы можете не видеть диалог установки приложения в браузере, если всплывающие окна отключены для браузера.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="4cd1c-132">Если это произойдет, в включить всплывающее окно и обновить страницу.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-132">If this happens, enable pop-up windows and refresh the page.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4cd1c-133">Дополнительные. Создание приложений с помощью кода Microsoft Teams набор средств и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4cd1c-133">Learn more: Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
