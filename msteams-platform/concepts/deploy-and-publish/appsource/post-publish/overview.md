---
title: Обслуживание и поддержка вашего опубликованного приложения
description: Что нужно думать о том, как только ваш магазин будет указан в Teams магазине и AppSource.
ms.topic: conceptual
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 8e4656ea7ca9f373123026a50ecb837d1a64e3fa
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230919"
---
# <a name="maintain-your-published-microsoft-teams-app"></a><span data-ttu-id="67b68-103">Ведение опубликованного Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="67b68-103">Maintain your published Microsoft Teams app</span></span>

<span data-ttu-id="67b68-104">С помощью приложения, перечисленного в Microsoft Teams магазине, начните думать о том, как вы будете поддерживать приложение в будущем и увеличить загрузки и использования.</span><span class="sxs-lookup"><span data-stu-id="67b68-104">With your app listed on the Microsoft Teams store, start thinking about how you'll maintain the app going forward and increase downloads and usage.</span></span>

## <a name="publish-updates-to-your-app"></a><span data-ttu-id="67b68-105">Публикация обновлений в приложении</span><span class="sxs-lookup"><span data-stu-id="67b68-105">Publish updates to your app</span></span>

<span data-ttu-id="67b68-106">Вы можете отправить изменения в приложение (например, новые функции или даже метаданные) в Центре партнеров.</span><span class="sxs-lookup"><span data-stu-id="67b68-106">You can submit changes to your app (such as new features or even metadata) in Partner Center.</span></span> <span data-ttu-id="67b68-107">Эти изменения требуют нового процесса проверки.</span><span class="sxs-lookup"><span data-stu-id="67b68-107">These changes requires a new review process.</span></span>

<span data-ttu-id="67b68-108">Убедитесь в следующем при публикации обновлений:</span><span class="sxs-lookup"><span data-stu-id="67b68-108">Ensure the following when publishing updates:</span></span>

* <span data-ttu-id="67b68-109">Не меняйте свой ID приложения.</span><span class="sxs-lookup"><span data-stu-id="67b68-109">Don't change your app ID.</span></span>
* <span data-ttu-id="67b68-110">Приумножная версия вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="67b68-110">Increment your app's version number.</span></span>
* <span data-ttu-id="67b68-111">В Центре партнеров не выберите **Добавить новое приложение** для обновления.</span><span class="sxs-lookup"><span data-stu-id="67b68-111">In Partner Center, don't select **Add a new app** to do the update.</span></span> <span data-ttu-id="67b68-112">Перейдите на страницу приложения.</span><span class="sxs-lookup"><span data-stu-id="67b68-112">Go to your app's page instead.</span></span>

### <a name="app-updates-requiring-user-consent"></a><span data-ttu-id="67b68-113">Обновления приложений, требующие согласия пользователя</span><span class="sxs-lookup"><span data-stu-id="67b68-113">App updates requiring user consent</span></span>

<span data-ttu-id="67b68-114">Когда пользователь устанавливает ваше приложение, он должен предоставить приложению разрешение на доступ к службам и сведениям, которые требуется для работы приложения.</span><span class="sxs-lookup"><span data-stu-id="67b68-114">When a user installs your app, they must give the app permission to access the services and information the app requires to function.</span></span> <span data-ttu-id="67b68-115">В большинстве случаев пользователям необходимо сделать это только один раз и автоматически установить новые версии приложения.</span><span class="sxs-lookup"><span data-stu-id="67b68-115">In most cases, users only have to do this once and new versions of your app install automatically.</span></span>

<span data-ttu-id="67b68-116">Однако при внесении каких-либо из следующих изменений в приложение существующие пользователи должны принять другой запрос на разрешение для установки обновления:</span><span class="sxs-lookup"><span data-stu-id="67b68-116">If you make any of the following changes to your app, however, your existing users must accept another permission request to install the update:</span></span>

* <span data-ttu-id="67b68-117">Добавьте или удалите бот.</span><span class="sxs-lookup"><span data-stu-id="67b68-117">Add or remove a bot.</span></span>
* <span data-ttu-id="67b68-118">Измените ID бота.</span><span class="sxs-lookup"><span data-stu-id="67b68-118">Change the bot ID.</span></span>
* <span data-ttu-id="67b68-119">Изменение конфигурации уведомлений бота в одну сторону.</span><span class="sxs-lookup"><span data-stu-id="67b68-119">Modify a bot's one-way notification configuration.</span></span>
* <span data-ttu-id="67b68-120">Измените поддержку бота для загрузки и загрузки файлов.</span><span class="sxs-lookup"><span data-stu-id="67b68-120">Modify a bot's support for uploading and downloading files.</span></span>
* <span data-ttu-id="67b68-121">Добавьте или удалите расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="67b68-121">Add or remove a messaging extension.</span></span>
* <span data-ttu-id="67b68-122">Добавьте личную вкладку.</span><span class="sxs-lookup"><span data-stu-id="67b68-122">Add a personal tab.</span></span>
* <span data-ttu-id="67b68-123">Добавьте вкладку канал и группу.</span><span class="sxs-lookup"><span data-stu-id="67b68-123">Add a channel and group tab.</span></span>
* <span data-ttu-id="67b68-124">Добавьте соединителю.</span><span class="sxs-lookup"><span data-stu-id="67b68-124">Add a connector.</span></span>
* <span data-ttu-id="67b68-125">Изменение конфигураций, связанных с регистрацией Azure Active Directory приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67b68-125">Modify configurations related to your Azure Active Directory (Azure AD) app registration.</span></span> <span data-ttu-id="67b68-126">Дополнительные сведения [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo) см. в .</span><span class="sxs-lookup"><span data-stu-id="67b68-126">For more information, see [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo).</span></span>

## <a name="fix-issues-with-your-published-app"></a><span data-ttu-id="67b68-127">Устранение проблем с опубликованным приложением</span><span class="sxs-lookup"><span data-stu-id="67b68-127">Fix issues with your published app</span></span>

<span data-ttu-id="67b68-128">Корпорация Майкрософт выполняет ежедневные тесты автоматизации в приложениях, перечисленных в Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="67b68-128">Microsoft runs daily automation tests on apps listed on the Teams store.</span></span> <span data-ttu-id="67b68-129">Если выявлены проблемы с приложением, мы обращаемся к вам с подробным отчетом о том, как воспроизвести проблемы и рекомендации по их устранению.</span><span class="sxs-lookup"><span data-stu-id="67b68-129">If issues with your app are identified, we contact you with a detailed report on how to reproduce the issues and recommendations to resolve them.</span></span> <span data-ttu-id="67b68-130">Если вы не можете устранить проблемы в заявленной временной шкале, список приложений может быть удален из магазина.</span><span class="sxs-lookup"><span data-stu-id="67b68-130">If you can't fix the problems within a stated timeline, your app listing may be removed from the store.</span></span>

## <a name="promote-your-app-on-another-site"></a><span data-ttu-id="67b68-131">Продвижение приложения на другом сайте</span><span class="sxs-lookup"><span data-stu-id="67b68-131">Promote your app on another site</span></span>

<span data-ttu-id="67b68-132">Когда приложение отображается в Teams магазине, можно создать ссылку, которая запускает Teams и отображает диалоговое окно для установки приложения.</span><span class="sxs-lookup"><span data-stu-id="67b68-132">When your app is listed in the Teams store, you can create a link that launches Teams and displays a dialog to install your app.</span></span> <span data-ttu-id="67b68-133">Эту ссылку можно включить, например, с помощью кнопки загрузки на странице маркетинга продукта.</span><span class="sxs-lookup"><span data-stu-id="67b68-133">You could include this link, for example, with a download button on your product's marketing page.</span></span>

<span data-ttu-id="67b68-134">Создайте ссылку, используя следующий URL-адрес, приданный вашему ID приложения: `https://teams.microsoft.com/l/app/<your-app-id>` .</span><span class="sxs-lookup"><span data-stu-id="67b68-134">Create the link using the following URL appended with your app ID: `https://teams.microsoft.com/l/app/<your-app-id>`.</span></span>

## <a name="complete-microsoft-365-certification"></a><span data-ttu-id="67b68-135">Полное Microsoft 365 сертификации</span><span class="sxs-lookup"><span data-stu-id="67b68-135">Complete Microsoft 365 Certification</span></span>

<span data-ttu-id="67b68-136">[Microsoft 365](/microsoft-365-app-certification/docs/certification) сертификация обеспечивает надлежащую защиту данных и конфиденциальности при установке сторонних Приложение Office или надстроек в вашей Microsoft 365 экосистеме.</span><span class="sxs-lookup"><span data-stu-id="67b68-136">[Microsoft 365 Certification](/microsoft-365-app-certification/docs/certification) offers assurances that data and privacy are adequately secured and protected when a third-party Office app or add-in is installed in your Microsoft 365 ecosystem.</span></span> <span data-ttu-id="67b68-137">Сертификация подтверждает, что ваше приложение совместимо с технологиями Майкрософт, соответствует требованиям безопасности облачных приложений и поддерживается Корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="67b68-137">Certification confirms that your app is compatible with Microsoft technologies, compliant with cloud app security best practices, and supported by Microsoft.</span></span>

## <a name="see-also"></a><span data-ttu-id="67b68-138">См. также</span><span class="sxs-lookup"><span data-stu-id="67b68-138">See also</span></span>

[<span data-ttu-id="67b68-139">Монетизация приложения через Microsoft Commercial Marketplace</span><span class="sxs-lookup"><span data-stu-id="67b68-139">Monetize your app through Microsoft Commercial Marketplace</span></span>](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
