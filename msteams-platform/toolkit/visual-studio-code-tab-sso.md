---
title: Одноэтажная аутентификация с Teams набор средств и Visual Studio Code для вкладок
description: Создайте вкладку, которая поддерживает одновокекай и Microsoft Graph звонки непосредственно в Visual Studio Code с Microsoft Teams набор средств
keywords: команды визуальный набор инструментов студии инструментарий вкладки sso граф аутентификации Azure платформы идентификации
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 11e642ce335dae4344f1c730b73763e9172fd76c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566833"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="21f76-104">Одноэтажная аутентификация с Teams набор средств и Visual Studio Code для вкладок</span><span class="sxs-lookup"><span data-stu-id="21f76-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="21f76-105">Система Microsoft Teams набор средств создать единую аутентификацию (SSO) для приложений вкладок непосредственно в пределах Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="21f76-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="21f76-106">Набор инструментов проведет вас через этот процесс и предоставляет все необходимое, включая платформа удостоверений Майкрософт регистрацию на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="21f76-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="21f76-107">Начать работу – создать проект</span><span class="sxs-lookup"><span data-stu-id="21f76-107">Get started — create a project</span></span>

1. <span data-ttu-id="21f76-108">Создайте новый проект в наборе инструментов.</span><span class="sxs-lookup"><span data-stu-id="21f76-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="21f76-109">Выберите вкладку в качестве типа расширения, который вы хотели бы создать.</span><span class="sxs-lookup"><span data-stu-id="21f76-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="21f76-110">Выберите опцию поддержки SSO.</span><span class="sxs-lookup"><span data-stu-id="21f76-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="21f76-111">После установки, вы должны Teams набор средств в Visual Studio Code деятельности.</span><span class="sxs-lookup"><span data-stu-id="21f76-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="21f76-112">Если нет, нажмите правой кнопкой мыши в баре активности **и выберите Microsoft Teams,** чтобы закрепить набор инструментов для легкого доступа.</span><span class="sxs-lookup"><span data-stu-id="21f76-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="21f76-113">Настройте свой проект</span><span class="sxs-lookup"><span data-stu-id="21f76-113">Configure your project</span></span>

1. <span data-ttu-id="21f76-114">Для включения SSO в Teams приложение должно иметь ресурс регистрации приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="21f76-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="21f76-115">Компания Teams набор средств будет предоставление регистрации приложения от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="21f76-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="21f76-116">Введите URL-адрес, где будет размещено ваше приложение, и выберите **следующий.**</span><span class="sxs-lookup"><span data-stu-id="21f76-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="21f76-117">Регистрация приложения будет настроена с использованием предоставленного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="21f76-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="21f76-118">Сведения о конфигурации приложения будут храниться в `.env` файлах в исходным коде проекта.</span><span class="sxs-lookup"><span data-stu-id="21f76-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="21f76-119">Если вы хотите узнать больше о том, как будет предусмотрена регистрация приложения Azure, _пожалуйста,_ можно найти нашу единую [поддержку документации вкладок (SSO).](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="21f76-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="21f76-120">Вам нужно будет перейти к **регистрации приложений Azure и** обновить *API URI и* перенаправить *URL-адреса всякий* раз, когда вы измените этот URL.</span><span class="sxs-lookup"><span data-stu-id="21f76-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="21f76-121">Запуск проекта</span><span class="sxs-lookup"><span data-stu-id="21f76-121">Run your project</span></span>

1. <span data-ttu-id="21f76-122">Выберите **npm установить** из `api-server` папки.</span><span class="sxs-lookup"><span data-stu-id="21f76-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="21f76-123">Затем **npm начать**.</span><span class="sxs-lookup"><span data-stu-id="21f76-123">Then **npm start**.</span></span>
1. <span data-ttu-id="21f76-124">Выберите **npm установить** из `.src` папки.</span><span class="sxs-lookup"><span data-stu-id="21f76-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="21f76-125">Затем **npm начать**.</span><span class="sxs-lookup"><span data-stu-id="21f76-125">Then **npm start**.</span></span>
1. <span data-ttu-id="21f76-126">Если вы используете туннельную службу, [такую как ngrok,](https://ngrok.com/)запустите ее и убедитесь, что URL совпадает с тем, что вы ввели в мастер создания проекта.</span><span class="sxs-lookup"><span data-stu-id="21f76-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="21f76-127">Если это не так, вам нужно будет обновить _API URI и перенаправить_ URL в _регистрации_ приложения, которое было создано в Azure.</span><span class="sxs-lookup"><span data-stu-id="21f76-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="21f76-128">Перейдите в бар активности на левой стороне Visual Studio Code окна.</span><span class="sxs-lookup"><span data-stu-id="21f76-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="21f76-129">Выберите **значок Run** для отображения **представления Run and Debug.**</span><span class="sxs-lookup"><span data-stu-id="21f76-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="21f76-130">Вы также можете использовать клавишу ярлык **Ctrl-Shift -D**.</span><span class="sxs-lookup"><span data-stu-id="21f76-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="21f76-131">Вы можете не видеть диалог установки приложения в браузере, если всплывающие окна отключены для вашего браузера.</span><span class="sxs-lookup"><span data-stu-id="21f76-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="21f76-132">Если это произойдет, включите всплывающие окна и обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="21f76-132">If this happens, enable pop-up windows and refresh the page.</span></span>

## <a name="see-also"></a><span data-ttu-id="21f76-133">См. также</span><span class="sxs-lookup"><span data-stu-id="21f76-133">See also</span></span>

- [<span data-ttu-id="21f76-134">Создавайте приложения с помощью Microsoft Teams набор средств и Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="21f76-134">Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
