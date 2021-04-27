---
title: Настройка поставщиков удостоверений OAuth 2.0
description: Описывает настройку поставщиков удостоверений с фокусом на Azure AD
ms.topic: how-to
localization_priority: Normal
keywords: teams authentication AAD oauth identity provider
ms.openlocfilehash: ffcf376ea6c4f1a94d797413af22af867dbd5b53
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020858"
---
# <a name="configure-identity-providers"></a><span data-ttu-id="4dd03-104">Настройка поставщиков удостоверений</span><span class="sxs-lookup"><span data-stu-id="4dd03-104">Configure identity providers</span></span>

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="4dd03-105">Настройка приложения для использования Azure Active Directory в качестве поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="4dd03-105">Configuring an application to use Azure Active Directory as an identity provider</span></span>

<span data-ttu-id="4dd03-106">Поставщики удостоверений, поддерживающие OAuth 2.0, не будут проверку подлинности запросов от неизвестных приложений; приложения должны быть зарегистрированы заранее.</span><span class="sxs-lookup"><span data-stu-id="4dd03-106">Identity providers supporting OAuth 2.0 will not authenticate requests from unknown applications; applications must be registered ahead of time.</span></span> <span data-ttu-id="4dd03-107">Чтобы сделать это с Azure AD, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4dd03-107">To do this with Azure AD, follow these steps:</span></span>

1. <span data-ttu-id="4dd03-108">Откройте [портал регистрации приложений.](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)</span><span class="sxs-lookup"><span data-stu-id="4dd03-108">Open the [Application Registration Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span></span>

2. <span data-ttu-id="4dd03-109">Выберите приложение, чтобы просмотреть его свойства, или нажмите кнопку "Новая регистрация".</span><span class="sxs-lookup"><span data-stu-id="4dd03-109">Select your app to view its properties, or click the "New Registration" button.</span></span> <span data-ttu-id="4dd03-110">Найдите **раздел URI** перенаправления для приложения.</span><span class="sxs-lookup"><span data-stu-id="4dd03-110">Find the **Redirect URI** section for the app.</span></span>

3. <span data-ttu-id="4dd03-111">В меню отсев убедитесь, что **выбран** Веб.</span><span class="sxs-lookup"><span data-stu-id="4dd03-111">In the dropdown menu, make sure **Web** is selected.</span></span> <span data-ttu-id="4dd03-112">Обновите URL-адрес конечной точки проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4dd03-112">Update the URL to your authentication endpoint.</span></span> <span data-ttu-id="4dd03-113">В примере typeScript/Node.js и C# GitHub URL-адреса перенаправления будут похожи на такие:</span><span class="sxs-lookup"><span data-stu-id="4dd03-113">For the TypeScript/Node.js and C# sample apps on GitHub, the redirect URLs will be similar to this:</span></span>

    <span data-ttu-id="4dd03-114">Url-адреса перенаправления: `https://<hostname>/bot-auth/simple-start`</span><span class="sxs-lookup"><span data-stu-id="4dd03-114">Redirect URLs: `https://<hostname>/bot-auth/simple-start`</span></span>

<span data-ttu-id="4dd03-115">Замените `<hostname>` фактическим хостом.</span><span class="sxs-lookup"><span data-stu-id="4dd03-115">Replace `<hostname>` with your actual host.</span></span> <span data-ttu-id="4dd03-116">Это может быть выделенный хостинг-сайт, например Azure, Glitch или туннель ngrok для localhost на компьютере разработки, например `abcd1234.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="4dd03-116">This might be a dedicated hosting site such as Azure, Glitch, or an ngrok tunnel to localhost on your development machine such as `abcd1234.ngrok.io`.</span></span> <span data-ttu-id="4dd03-117">Вы можете еще не иметь эту информацию, если вы еще не завершили или не выполнили хостинг приложения (или примера приложения, упомянутого выше), но вы всегда можете вернуться на эту страницу, когда эта информация будет известна.</span><span class="sxs-lookup"><span data-stu-id="4dd03-117">You may not have this information yet if you have not completed or hosted your app (or the sample app mentioned above), but you can always return to this page when that information is known.</span></span>

## <a name="other-authentication-providers"></a><span data-ttu-id="4dd03-118">Другие поставщики проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="4dd03-118">Other authentication providers</span></span>

* <span data-ttu-id="4dd03-119">**LinkedIn** Следуйте инструкциям в [настройке приложения LinkedIn](/linkedin/talent/apply-with-linkedin)</span><span class="sxs-lookup"><span data-stu-id="4dd03-119">**LinkedIn** Follow the instructions in [Configuring your LinkedIn application](/linkedin/talent/apply-with-linkedin)</span></span>

* <span data-ttu-id="4dd03-120">**Google** Получение учетных данных клиента OAuth 2.0 из [консоли API Google](https://console.developers.google.com/)</span><span class="sxs-lookup"><span data-stu-id="4dd03-120">**Google** Obtain OAuth 2.0 client credentials from the [Google API Console](https://console.developers.google.com/)</span></span>
