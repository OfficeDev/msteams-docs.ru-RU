---
title: Проверка подлинности единого входа с помощью набора инструментов Teams и кода Visual Studio для вкладок
description: Создание вкладки, поддерживающей единый вход, и вызовов Microsoft Graph непосредственно в Visual Studio Code с помощью набора инструментов Microsoft Teams
keywords: вкладки набора средств Visual Studio Code Toolkit в Visual Studio Graph проверка подлинности для платформы удостоверений Azure
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: fe734143975688cd35c510cd68cd0779a2200a18
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/30/2020
ms.locfileid: "49477738"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="24737-104">Проверка подлинности единого входа с помощью набора инструментов Teams и кода Visual Studio для вкладок</span><span class="sxs-lookup"><span data-stu-id="24737-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="24737-105">Набор средств Microsoft Teams позволяет создать проверку подлинности единого входа для приложений вкладок непосредственно в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="24737-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="24737-106">Набор средств поможет вам выполнить весь процесс и предоставляет все необходимое, включая подготовку регистрации платформы идентификации Майкрософт на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="24737-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="24737-107">Приступая к работе — создание проекта</span><span class="sxs-lookup"><span data-stu-id="24737-107">Get started — create a project</span></span>

1. <span data-ttu-id="24737-108">Создайте новый проект в наборе инструментов.</span><span class="sxs-lookup"><span data-stu-id="24737-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="24737-109">Выберите вкладку в качестве типа расширения, которое вы хотите создать.</span><span class="sxs-lookup"><span data-stu-id="24737-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="24737-110">Выберите параметр для поддержки единого входа.</span><span class="sxs-lookup"><span data-stu-id="24737-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="24737-111">После установки вы должны увидеть набор инструментов Teams на панели действий Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="24737-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="24737-112">Если это не так, щелкните правой кнопкой мыши на панели действий и выберите **Microsoft Teams** , чтобы закрепить набор инструментов для упрощения доступа.</span><span class="sxs-lookup"><span data-stu-id="24737-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="24737-113">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="24737-113">Configure your project</span></span>

1. <span data-ttu-id="24737-114">Чтобы включить единый вход в Teams, ваше приложение должно иметь ресурс регистрации приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="24737-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="24737-115">Набор инструментов Teams выполнит подготовку к регистрации приложения от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="24737-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="24737-116">Введите URL-адрес, где будет размещаться ваше приложение, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="24737-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="24737-117">Регистрационное приложение будет настроено с использованием предоставленного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="24737-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="24737-118">Сведения о конфигурации регистрации приложения будут храниться в `.env` файлах исходного кода проекта.</span><span class="sxs-lookup"><span data-stu-id="24737-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="24737-119">Если вы хотите узнать больше о том, как будет подготовлена регистрация приложения Azure, _Ознакомьтесь_  со статьей [Поддержка единого входа (SSO)](../tabs/how-to/authentication/auth-aad-sso.md) в документации по вкладкам.</span><span class="sxs-lookup"><span data-stu-id="24737-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="24737-120">Вам потребуется перейти в службу **регистрации приложений Azure** и обновить *URI API* и *перенаправить URL-адреса* при каждом изменении этого URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="24737-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="24737-121">Запуск проекта</span><span class="sxs-lookup"><span data-stu-id="24737-121">Run your project</span></span>

1. <span data-ttu-id="24737-122">Выберите **NPM установки** из `api-server` папки.</span><span class="sxs-lookup"><span data-stu-id="24737-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="24737-123">Затем **NPM Start**.</span><span class="sxs-lookup"><span data-stu-id="24737-123">Then **npm start**.</span></span>
1. <span data-ttu-id="24737-124">Выберите **NPM установки** из `.src` папки.</span><span class="sxs-lookup"><span data-stu-id="24737-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="24737-125">Затем **NPM Start**.</span><span class="sxs-lookup"><span data-stu-id="24737-125">Then **npm start**.</span></span>
1. <span data-ttu-id="24737-126">При использовании службы туннелирования, такой как [ngrok](https://ngrok.com/), запустите ее и убедитесь, что URL-адрес совпадает с указанным в мастере создания проекта.</span><span class="sxs-lookup"><span data-stu-id="24737-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="24737-127">Если это не так, вам потребуется обновить _URI API_ и _URL-адрес перенаправления_ в регистрации приложения, созданного в Azure.</span><span class="sxs-lookup"><span data-stu-id="24737-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="24737-128">Перейдите на панель действий в левой части окна кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24737-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="24737-129">Выберите значок **Run (выполнить** ) для отображения представления " **Запуск" и "Отладка** ".</span><span class="sxs-lookup"><span data-stu-id="24737-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="24737-130">Вы также можете использовать сочетание клавиш **CTRL + SHIFT + D**.</span><span class="sxs-lookup"><span data-stu-id="24737-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="24737-131">Если в браузере отключены всплывающие окна установки приложения, диалоговое окно установки приложения отображаться не будет.</span><span class="sxs-lookup"><span data-stu-id="24737-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="24737-132">Если это произойдет, включите всплывающие окна и обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="24737-132">If this happens, enable pop-up windows and refresh the page.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="24737-133">Дополнительные сведения: создание приложений с помощью набора инструментов Microsoft Teams и кода Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24737-133">Learn more: Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
