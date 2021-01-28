---
title: Обслуживание и поддержка опубликованного приложения
description: Что делать после публикации приложения
ms.topic: how-to
keywords: Манифест обновления сертификации обновлений приложений после публикации teams
ms.openlocfilehash: ce63b840307f7e12a5cd05a1c67aed017cf6199b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014329"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="ab0ed-104">Обслуживание и поддержка вашего опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="ab0ed-104">Maintain and support your published app</span></span> 

<span data-ttu-id="ab0ed-105">После утверждения приложения и его добавления в общедоступный каталог приложений вы можете повысить свою охват, выполив программу соответствия требованиям приложений Microsoft 365 или добавив кнопку скачивания на свой веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="microsoft-365-certified"></a><span data-ttu-id="ab0ed-106">Сертификация Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="ab0ed-106">Microsoft 365 Certified</span></span>

<span data-ttu-id="ab0ed-107">Программа соответствия требованиям приложений [Microsoft 365](./application-certification.md)— это трехуровневый подход к обеспечению безопасности и соответствия требованиям приложений.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="ab0ed-108">Каждый уровень построен на следующем — предлагая многоуровневую программу для удовлетворения потребностей клиента.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="ab0ed-109">Вы можете узнать больше о состоянии безопасности и соответствия требованиям приложений Teams, посетив страницу [соответствия](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)требованиям.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="ab0ed-110">Добавление кнопки скачивания на сайт продукта</span><span class="sxs-lookup"><span data-stu-id="ab0ed-110">Add a download button to your product site</span></span>

<span data-ttu-id="ab0ed-111">Если ваше приложение находится в глобальном магазине Microsoft Teams, вы можете создать ссылку для своего веб-сайта, который запускает Teams и отображает диалоговое окно согласия и установки для добавления приложения пользователями.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-111">If your app is in the Microsoft Teams global store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="ab0ed-112">Формат:  `https://teams.microsoft.com/l/app/<appId>` где appID — это GUID, объявленный в отправленном манифесте.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="ab0ed-113">Пример: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` ссылка для установки Trello.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="ab0ed-114">Обновление существующего приложения Teams</span><span class="sxs-lookup"><span data-stu-id="ab0ed-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="ab0ed-115">Не используйте *кнопку "Добавить новое приложение",* чтобы повторно отправить приложение.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="ab0ed-116">Используйте плитку для приложения на вкладке "Обзор".</span><span class="sxs-lookup"><span data-stu-id="ab0ed-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="ab0ed-117">AppId в обновленном манифесте должен быть таким же, как в текущем манифесте, с номером версии.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="ab0ed-118">При внесении каких-либо изменений в отправку, включая имя приложения или метаданные в манифесте, помнозите номер версии в манифесте.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-118">Increment your version number in the manifest if you make any changes to your submission including app name or any metadata in the manifest.</span></span>
* <span data-ttu-id="ab0ed-119">Обновленные отправки необходимы для прохождения нового процесса проверки и проверки.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="ab0ed-120">Обновления приложения и поток согласия пользователя</span><span class="sxs-lookup"><span data-stu-id="ab0ed-120">App updates and the user consent flow</span></span>

<span data-ttu-id="ab0ed-121">Когда пользователь устанавливает ваше приложение, одно из первых его действия — предоставить приложению разрешение на доступ к службам и сведения, необходимые приложению для его работы.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="ab0ed-122">В большинстве случаев после завершения обновления приложения новая версия будет автоматически отображаться для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="ab0ed-123">Однако существуют некоторые обновления манифеста [приложения Teams,](../../../../resources/schema/manifest-schema.md) которые требуют принятия пользователем для завершения и могут повторно запускать такое поведение согласия:</span><span class="sxs-lookup"><span data-stu-id="ab0ed-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="ab0ed-124">Бот был добавлен или удален.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-124">A bot was added or removed.</span></span>
> * <span data-ttu-id="ab0ed-125">Уникальное значение существующего бота `botId` изменено.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-125">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="ab0ed-126">Boolean-значение существующего `isNotificationOnly` бота изменено.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-126">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="ab0ed-127">Boolean-значение существующего `supportsFiles` бота изменено.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-127">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="ab0ed-128">Добавлено или удалено расширение обмена сообщениями ( `composeExtensions` ).</span><span class="sxs-lookup"><span data-stu-id="ab0ed-128">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="ab0ed-129">Добавлен новый соединител.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-129">A new connector was added.</span></span>
> * <span data-ttu-id="ab0ed-130">Добавлена новая статическая/личная вкладка.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-130">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="ab0ed-131">Добавлена новая настраиваемая вкладка "Группа/канал".</span><span class="sxs-lookup"><span data-stu-id="ab0ed-131">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="ab0ed-132">Значения `webApplicationInfo` изменились.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-132">The `webApplicationInfo` values changed.</span></span>
>

### <a name="images-of-user-consent-flow"></a><span data-ttu-id="ab0ed-133">Изображения потока согласия пользователя:</span><span class="sxs-lookup"><span data-stu-id="ab0ed-133">Images of user consent flow:</span></span>

<span data-ttu-id="ab0ed-134">**Настройка соединители —** этот экран будет отображаться только для пользователей Teams.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-134">**Set up a connector** —  This screen will appear only for Teams users.</span></span>

![Схема настройки соединители с потоком согласия](../../../../assets/images/connector-teams-consentflow.png)

<span data-ttu-id="ab0ed-136">**Поток согласия пользователя** — этот экран часто используется как для личных, так и для групповых областей.</span><span class="sxs-lookup"><span data-stu-id="ab0ed-136">**User consent flow** - This screen is common for both personal and group scope.</span></span> <span data-ttu-id="ab0ed-137">Здесь выберите **"Согласие" от имени вашей** организации и выберите **"Принять".**</span><span class="sxs-lookup"><span data-stu-id="ab0ed-137">Here, select the **Consent on behalf of your organization** checkbox and choose **Accept**.</span></span>

![Схема разрешений](../../../../assets/images/user-consent-flow.png)
