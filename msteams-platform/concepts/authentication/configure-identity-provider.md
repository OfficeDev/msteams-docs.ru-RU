---
title: Настройка поставщиков удостоверений OAuth 2.0
description: В этой статье описывается настройка поставщиков удостоверений с фокусом на Azure AD
ms.topic: how-to
keywords: поставщик удостоверений AAD oauth для проверки подлинности teams
ms.openlocfilehash: b5ffd6c4c1edd2c4315ea1e31474a626de53aba1
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014469"
---
# <a name="configure-identity-providers"></a><span data-ttu-id="15970-104">Настройка поставщиков удостоверений</span><span class="sxs-lookup"><span data-stu-id="15970-104">Configure identity providers</span></span>

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="15970-105">Настройка приложения для использования Azure Active Directory в качестве поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="15970-105">Configuring an application to use Azure Active Directory as an identity provider</span></span>

<span data-ttu-id="15970-106">Поставщики удостоверений, поддерживающие OAuth 2.0, не будут проверку подлинности запросов из неизвестных приложений; приложения должны быть зарегистрированы заранее.</span><span class="sxs-lookup"><span data-stu-id="15970-106">Identity providers supporting OAuth 2.0 will not authenticate requests from unknown applications; applications must be registered ahead of time.</span></span> <span data-ttu-id="15970-107">Чтобы сделать это с помощью Azure AD, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="15970-107">To do this with Azure AD, follow these steps:</span></span>

1. <span data-ttu-id="15970-108">Откройте портал [регистрации приложений.](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)</span><span class="sxs-lookup"><span data-stu-id="15970-108">Open the [Application Registration Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span></span>

2. <span data-ttu-id="15970-109">Выберите приложение, чтобы просмотреть его свойства, или нажмите кнопку "Новая регистрация".</span><span class="sxs-lookup"><span data-stu-id="15970-109">Select your app to view its properties, or click the "New Registration" button.</span></span> <span data-ttu-id="15970-110">Найдите **раздел URI** перенаправления для приложения.</span><span class="sxs-lookup"><span data-stu-id="15970-110">Find the **Redirect URI** section for the app.</span></span>

3. <span data-ttu-id="15970-111">Убедитесь, что в  меню в меню "Интернет" выбран веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="15970-111">In the dropdown menu, make sure **Web** is selected.</span></span> <span data-ttu-id="15970-112">Обновите URL-адрес конечной точки проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="15970-112">Update the URL to your authentication endpoint.</span></span> <span data-ttu-id="15970-113">Для примеров приложений TypeScript/Node.js и C# на GitHub URL-адреса перенаправления будут иметь примерно такой вид:</span><span class="sxs-lookup"><span data-stu-id="15970-113">For the TypeScript/Node.js and C# sample apps on GitHub, the redirect URLs will be similar to this:</span></span>

    <span data-ttu-id="15970-114">URL-адреса перенаправления: `https://<hostname>/bot-auth/simple-start`</span><span class="sxs-lookup"><span data-stu-id="15970-114">Redirect URLs: `https://<hostname>/bot-auth/simple-start`</span></span>

<span data-ttu-id="15970-115">Замените `<hostname>` фактический хост.</span><span class="sxs-lookup"><span data-stu-id="15970-115">Replace `<hostname>` with your actual host.</span></span> <span data-ttu-id="15970-116">Это может быть выделенный сайт размещения, например Azure, Glitch или туннель ngrok для localhost на вашем компьютере разработки, например `abcd1234.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="15970-116">This might be a dedicated hosting site such as Azure, Glitch, or an ngrok tunnel to localhost on your development machine such as `abcd1234.ngrok.io`.</span></span> <span data-ttu-id="15970-117">Возможно, у вас пока нет этих сведений, если вы еще не завершили или не развернетесь в приложении (или в примере приложения, упомянутом выше), но вы всегда можете вернуться на эту страницу, если эти сведения известны.</span><span class="sxs-lookup"><span data-stu-id="15970-117">You may not have this information yet if you have not completed or hosted your app (or the sample app mentioned above), but you can always return to this page when that information is known.</span></span>

## <a name="other-authentication-providers"></a><span data-ttu-id="15970-118">Другие поставщики проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="15970-118">Other authentication providers</span></span>

* <span data-ttu-id="15970-119">**LinkedIn** Следуйте инструкциям по [настройке приложения LinkedIn](https://developer.linkedin.com/docs/oauth2)</span><span class="sxs-lookup"><span data-stu-id="15970-119">**LinkedIn** Follow the instructions in [Configuring your LinkedIn application](https://developer.linkedin.com/docs/oauth2)</span></span>

* <span data-ttu-id="15970-120">**Google** Получение учетных данных клиента OAuth 2.0 из консоли [API Google](https://console.developers.google.com/)</span><span class="sxs-lookup"><span data-stu-id="15970-120">**Google** Obtain OAuth 2.0 client credentials from the [Google API Console](https://console.developers.google.com/)</span></span>
