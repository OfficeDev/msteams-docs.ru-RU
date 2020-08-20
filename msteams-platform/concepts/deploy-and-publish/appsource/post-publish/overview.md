---
title: Публикация после публикации
description: Что делать после публикации приложения
keywords: Teams post post update certificate
ms.openlocfilehash: d2cc6c5427c5b4f7320f0ec2e022f2c69467a33d
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819156"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="9c2e8-104">Обслуживание и поддержка вашего опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="9c2e8-104">Maintain and support your published app</span></span> 

<span data-ttu-id="9c2e8-105">После утверждения приложения и его добавления в общедоступный каталог приложений вы можете расширить эту аудиторию, заполнив программу по соответствию требованиям приложений Microsoft 365 или нажав кнопку скачивания на своем сайте.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="microsoft-365-certified"></a><span data-ttu-id="9c2e8-106">Сертифицировано ее использование microsoft 365</span><span class="sxs-lookup"><span data-stu-id="9c2e8-106">Microsoft 365 Certified</span></span>

<span data-ttu-id="9c2e8-107">Программа [соответствия приложений Microsoft 365](./application-certification.md)— это три уровня безопасности приложений и обеспечения соответствия требованиям.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="9c2e8-108">Каждый уровень построен на следующий и предлагает многоуровневую программу в соответствии с потребностями клиентов.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="9c2e8-109">Чтобы узнать больше о плане безопасности и соответствия требованиям приложений Teams, посетите страницу [соответствия требованиям.](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)</span><span class="sxs-lookup"><span data-stu-id="9c2e8-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="9c2e8-110">Добавление кнопки скачивания на сайт продукта</span><span class="sxs-lookup"><span data-stu-id="9c2e8-110">Add a download button to your product site</span></span>

<span data-ttu-id="9c2e8-111">Если ваше приложение находится в хранилище Microsoft Teams, вы можете создать ссылку на ваш веб-сайт, которая открывает Teams и диалоговое окно согласия и установки, в котором пользователи могут добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-111">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="9c2e8-112">Формат:  `https://teams.microsoft.com/l/app/<appId>` AppID — это GUID, объявленный в отправленном манифесте.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="9c2e8-113">Пример: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` ссылка для установки Trello.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="9c2e8-114">Обновление существующего приложения Teams</span><span class="sxs-lookup"><span data-stu-id="9c2e8-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="9c2e8-115">Не используйте *кнопку "Добавить новое приложение"* для повторной отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="9c2e8-116">Вместо этого используйте плитку для своего приложения на вкладке "Обзор".</span><span class="sxs-lookup"><span data-stu-id="9c2e8-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="9c2e8-117">Значение appId в обновленном манифесте должно совпадать с кодом, указанным в текущем манифесте, с последующим номером версии.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="9c2e8-118">Если в вашу отправку вносится манифест, надо будет менять номера версии в манифесте.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-118">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="9c2e8-119">Новые процессы проверки и проверки требуют ся обновленные отправленные решения.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="9c2e8-120">Обновление приложений и поток согласия пользователя</span><span class="sxs-lookup"><span data-stu-id="9c2e8-120">App updates and the user consent flow</span></span>

<span data-ttu-id="9c2e8-121">Первое, что пользователь устанавливает ваше приложение, вы предоставите приложению разрешение на доступ к службам и сведениям, необходимым приложению для выполнения поставленных задач.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="9c2e8-122">В большинстве случаев после обновления версии приложения новая версия автоматически отобразится для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="9c2e8-123">Однако существуют некоторые обновления манифеста [приложения Teams,](../../../../resources/schema/manifest-schema.md) которые требуют от пользователя дока закончиваться, и могут срабатывать повторно указанные ниже изменения поведения согласия.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="9c2e8-124">Был добавлен или удален бот.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-124">A bot was added or removed.</span></span>
> * <span data-ttu-id="9c2e8-125">Изменено уникальное значение `botId` существующего бота.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-125">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="9c2e8-126">Логическое значение существующего `isNotificationOnly` бота менялось.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-126">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="9c2e8-127">Логическое значение существующего `supportsFiles` бота менялось.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-127">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="9c2e8-128">Добавлено или `composeExtensions` удалено расширение сообщения ( ).</span><span class="sxs-lookup"><span data-stu-id="9c2e8-128">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="9c2e8-129">Был добавлен новый соединитель.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-129">A new connector was added.</span></span>
> * <span data-ttu-id="9c2e8-130">Добавлена новая статическая или персональная вкладка.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-130">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="9c2e8-131">Добавлена новая настраиваемая вкладка группы или канала.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-131">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="9c2e8-132">Изменены `webApplicationInfo` значения.</span><span class="sxs-lookup"><span data-stu-id="9c2e8-132">The `webApplicationInfo` values changed.</span></span>
>
