---
title: Настройка поставщиков удостоверений OAuth 2,0
description: В этой статье описывается настройка поставщиков удостоверений с фокусом на Azure AD
keywords: поставщик удостоверений AAD OAuth для проверки подлинности Teams
ms.openlocfilehash: 799b0c20cda64456a4610acbdbedf758989bee55
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675549"
---
# <a name="configuring-identity-providers"></a><span data-ttu-id="243fb-104">Настройка поставщиков удостоверений</span><span class="sxs-lookup"><span data-stu-id="243fb-104">Configuring identity providers</span></span>

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="243fb-105">Настройка приложения для использования Azure Active Directory в качестве поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="243fb-105">Configuring an application to use Azure Active Directory as an identity provider</span></span>

<span data-ttu-id="243fb-106">Поставщики удостоверений, поддерживающие OAuth 2,0, не будут выполнять проверку подлинности запросов от неизвестных приложений; приложения должны быть зарегистрированы заранее.</span><span class="sxs-lookup"><span data-stu-id="243fb-106">Identity providers supporting OAuth 2.0 will not authenticate requests from unknown applications; applications must be registered ahead of time.</span></span> <span data-ttu-id="243fb-107">Чтобы сделать это с помощью Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="243fb-107">To do this with Azure AD, follow these steps:</span></span>

1. <span data-ttu-id="243fb-108">Откройте [портал регистрации приложений](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span><span class="sxs-lookup"><span data-stu-id="243fb-108">Open the [Application Registration Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span></span>

2. <span data-ttu-id="243fb-109">Выберите свое приложение, чтобы просмотреть его свойства, или нажмите кнопку "создать регистрацию".</span><span class="sxs-lookup"><span data-stu-id="243fb-109">Select your app to view its properties, or click the "New Registration" button.</span></span> <span data-ttu-id="243fb-110">Найдите раздел **URI перенаправления** для приложения.</span><span class="sxs-lookup"><span data-stu-id="243fb-110">Find the **Redirect URI** section for the app.</span></span>

3. <span data-ttu-id="243fb-111">Убедитесь, что в раскрывающемся меню выбран пункт **веб** .</span><span class="sxs-lookup"><span data-stu-id="243fb-111">In the dropdown menu, make sure **Web** is selected.</span></span> <span data-ttu-id="243fb-112">Обновите URL-адрес конечной точки проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="243fb-112">Update the URL to your authentication endpoint.</span></span> <span data-ttu-id="243fb-113">Для примеров приложений TypeScript/Node. js и C# на сайте GitHub URL-адреса перенаправления будут выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="243fb-113">For the TypeScript/Node.js and C# sample apps on GitHub, the redirect URLs will be similar to this:</span></span>

    <span data-ttu-id="243fb-114">URL-адреса перенаправления:`https://<hostname>/bot-auth/simple-start`</span><span class="sxs-lookup"><span data-stu-id="243fb-114">Redirect URLs: `https://<hostname>/bot-auth/simple-start`</span></span>

<span data-ttu-id="243fb-115">Замените `<hostname>` фактическим узлом.</span><span class="sxs-lookup"><span data-stu-id="243fb-115">Replace `<hostname>` with your actual host.</span></span> <span data-ttu-id="243fb-116">Это может быть выделенный сайт, такой как Azure, сбой, или ngrok туннель для localhost на компьютере для разработки, `abcd1234.ngrok.io`например.</span><span class="sxs-lookup"><span data-stu-id="243fb-116">This might be a dedicated hosting site such as Azure, Glitch, or an ngrok tunnel to localhost on your development machine such as `abcd1234.ngrok.io`.</span></span> <span data-ttu-id="243fb-117">Эта информация может отсутствовать, если вы не выполнили или не развернули ваше приложение (или пример приложения, упомянутого выше), но всегда можете вернуться на эту страницу, если эта информация известна.</span><span class="sxs-lookup"><span data-stu-id="243fb-117">You may not have this information yet if you have not completed or hosted your app (or the sample app mentioned above), but you can always return to this page when that information is known.</span></span>

## <a name="other-authentication-providers"></a><span data-ttu-id="243fb-118">Другие поставщики проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="243fb-118">Other authentication providers</span></span>

* <span data-ttu-id="243fb-119">**LinkedIn** Следуйте инструкциям в статье [Настройка приложения LinkedIn](https://developer.linkedin.com/docs/oauth2)</span><span class="sxs-lookup"><span data-stu-id="243fb-119">**LinkedIn** Follow the instructions in [Configuring your LinkedIn application](https://developer.linkedin.com/docs/oauth2)</span></span>

* <span data-ttu-id="243fb-120">**Google** Получение учетных данных клиента OAuth 2,0 из [консоли Google API](https://console.developers.google.com/)</span><span class="sxs-lookup"><span data-stu-id="243fb-120">**Google** Obtain OAuth 2.0 client credentials from the [Google API Console](https://console.developers.google.com/)</span></span>
