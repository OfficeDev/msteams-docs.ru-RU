---
title: Ведение и поддержка опубликованного приложения
description: Что делать после публикации приложения
ms.topic: how-to
keywords: группы после публикации манифеста обновления приложений сертификации
ms.openlocfilehash: 8644db5e329e15d77062553eda4a41a36b2740ee
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585836"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="43f19-104">Обслуживание и поддержка вашего опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="43f19-104">Maintain and support your published app</span></span> 

<span data-ttu-id="43f19-105">После утверждения и перечисления приложения в каталоге общедоступных приложений вы можете увеличить охват, завершив программу соответствия требованиям к приложениям Microsoft 365 или добавив кнопку загрузки на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="43f19-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="microsoft-365-certified"></a><span data-ttu-id="43f19-106">Сертификация Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="43f19-106">Microsoft 365 Certified</span></span>

<span data-ttu-id="43f19-107">Программа соответствия требованиям к приложениям Microsoft [365](./application-certification.md)— это трехуровневый подход к обеспечению безопасности и соответствия требованиям приложений.</span><span class="sxs-lookup"><span data-stu-id="43f19-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="43f19-108">Каждый уровень строится на следующем уровне, предлагая многоуровневую программу для удовлетворения потребностей клиента.</span><span class="sxs-lookup"><span data-stu-id="43f19-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="43f19-109">Дополнительные информацию о состоянии безопасности и соответствия требованиям приложений Teams можно узнать, посетив страницу [соответствия](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)требованиям.</span><span class="sxs-lookup"><span data-stu-id="43f19-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="43f19-110">Добавление кнопки загрузки на сайт продукта</span><span class="sxs-lookup"><span data-stu-id="43f19-110">Add a download button to your product site</span></span>

<span data-ttu-id="43f19-111">Если ваше приложение находится в глобальном магазине Microsoft Teams, вы можете создать ссылку для веб-сайта, который запускает Teams и показывает диалоговое окно согласия и установки для пользователей, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="43f19-111">If your app is in the Microsoft Teams global store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="43f19-112">Формат:  `https://teams.microsoft.com/l/app/<appId>` где appID является GUID, который они объявляют в отправленном манифесте.</span><span class="sxs-lookup"><span data-stu-id="43f19-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="43f19-113">Пример: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` это ссылка на установку Trello.</span><span class="sxs-lookup"><span data-stu-id="43f19-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="43f19-114">Обновление существующего приложения Teams</span><span class="sxs-lookup"><span data-stu-id="43f19-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="43f19-115">Не используйте *кнопку Добавить новое приложение,* чтобы повторно отправить приложение.</span><span class="sxs-lookup"><span data-stu-id="43f19-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="43f19-116">Вместо этого используйте плитку для приложения на вкладке Обзор.</span><span class="sxs-lookup"><span data-stu-id="43f19-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="43f19-117">Приложение в обновленном манифесте должно быть таким же, как и в текущем манифесте, с дополнительным номером версии.</span><span class="sxs-lookup"><span data-stu-id="43f19-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="43f19-118">При внесении каких-либо изменений в представление, включая имя приложения или метаданные в манифесте, приумнозить номер версии в манифесте.</span><span class="sxs-lookup"><span data-stu-id="43f19-118">Increment your version number in the manifest if you make any changes to your submission including app name or any metadata in the manifest.</span></span>
* <span data-ttu-id="43f19-119">Обновленные материалы должны пройти новый процесс проверки и проверки.</span><span class="sxs-lookup"><span data-stu-id="43f19-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="43f19-120">Обновления приложений и поток согласия пользователей</span><span class="sxs-lookup"><span data-stu-id="43f19-120">App updates and the user consent flow</span></span>

<span data-ttu-id="43f19-121">Когда пользователь устанавливает приложение, одно из первых вещей, которое он должен сделать, это дать приложению разрешение на доступ к службам и сведениям, которые приложение должно делать свою работу.</span><span class="sxs-lookup"><span data-stu-id="43f19-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="43f19-122">В большинстве случаев после завершения обновления приложения новая версия будет автоматически отображаться для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="43f19-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="43f19-123">Однако есть некоторые обновления манифеста [приложения Teams,](../../../../resources/schema/manifest-schema.md) которые требуют принятия пользователей для завершения и могут повторно вызвать такое поведение согласия:</span><span class="sxs-lookup"><span data-stu-id="43f19-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="43f19-124">Бот добавляется или удаляется.</span><span class="sxs-lookup"><span data-stu-id="43f19-124">A bot is added or removed.</span></span>
> * <span data-ttu-id="43f19-125">Уникальное значение существующего `botId` бота изменено.</span><span class="sxs-lookup"><span data-stu-id="43f19-125">An existing bot's unique `botId` value is changed.</span></span>
> * <span data-ttu-id="43f19-126">Значение boolean существующего `isNotificationOnly` бота меняется.</span><span class="sxs-lookup"><span data-stu-id="43f19-126">An existing bot's `isNotificationOnly` boolean value is changed.</span></span>
> * <span data-ttu-id="43f19-127">Изменено существующее `supportsFiles` значение `supportsCalling` бота или boolean.</span><span class="sxs-lookup"><span data-stu-id="43f19-127">An existing bot's `supportsFiles` or `supportsCalling` boolean value is changed.</span></span>
> * <span data-ttu-id="43f19-128">Расширение обмена сообщениями `composeExtensions` добавляется или удаляется.</span><span class="sxs-lookup"><span data-stu-id="43f19-128">A messaging extension `composeExtensions` is added or removed.</span></span>
> * <span data-ttu-id="43f19-129">Добавлен новый соединитектор.</span><span class="sxs-lookup"><span data-stu-id="43f19-129">A new connector is added.</span></span>
> * <span data-ttu-id="43f19-130">Добавлена новая статическая или личная вкладка.</span><span class="sxs-lookup"><span data-stu-id="43f19-130">A new static or personal tab is added.</span></span>
> * <span data-ttu-id="43f19-131">Добавлена новая настраиваемая группа или вкладка канала.</span><span class="sxs-lookup"><span data-stu-id="43f19-131">A new configurable group or channel tab is added.</span></span>
> * <span data-ttu-id="43f19-132">Свойства внутри `webApplicationInfo` изменены.</span><span class="sxs-lookup"><span data-stu-id="43f19-132">The properties inside `webApplicationInfo` are changed.</span></span> <span data-ttu-id="43f19-133">Для изменений в области Teams требуется `webApplicationInfo` согласие.</span><span class="sxs-lookup"><span data-stu-id="43f19-133">For changes to `webApplicationInfo`, consent is only required in the Teams scope.</span></span>

### <a name="images-of-user-consent-flow"></a><span data-ttu-id="43f19-134">Изображения потока согласия пользователя:</span><span class="sxs-lookup"><span data-stu-id="43f19-134">Images of user consent flow:</span></span>

<span data-ttu-id="43f19-135">**Настройка соединитетеля** — этот экран будет отображаться только для пользователей Teams.</span><span class="sxs-lookup"><span data-stu-id="43f19-135">**Set up a connector** —  This screen will appear only for Teams users.</span></span>

![Настройка схемы соединитетеля потока согласия](../../../../assets/images/connector-teams-consentflow.png)

<span data-ttu-id="43f19-137">**Поток согласия пользователя** — этот экран является общим как для личных, так и для групповых областей.</span><span class="sxs-lookup"><span data-stu-id="43f19-137">**User consent flow** - This screen is common for both personal and group scope.</span></span> <span data-ttu-id="43f19-138">Здесь выберите **Согласие от имени вашего** почтового ящика организации и выберите **Accept**.</span><span class="sxs-lookup"><span data-stu-id="43f19-138">Here, select the **Consent on behalf of your organization** checkbox and choose **Accept**.</span></span>

![Схема разрешений](../../../../assets/images/user-consent-flow.png)
