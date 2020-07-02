---
title: Публикация после публикации
description: Что делать после публикации приложения
keywords: сертификат обновления публикаций после публикации Teams
ms.openlocfilehash: 887e18ac7e27cf12aa4319ac240e42f21f05fd75
ms.sourcegitcommit: e355f59d2d21a2d5ae36cc46acad5ed4765b42e0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "45021575"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="ca974-104">Обслуживание и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="ca974-104">Maintain and support your published app</span></span> 

<span data-ttu-id="ca974-105">Когда ваше приложение будет утверждено и указано в общедоступном каталоге приложений, вы можете увеличить его, выполнив программу Microsoft 365 для приложений на соответствие требованиям или добавив кнопку скачать на свой веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="ca974-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="m365-certified"></a><span data-ttu-id="ca974-106">Сертифицированный M365</span><span class="sxs-lookup"><span data-stu-id="ca974-106">M365 Certified</span></span>

<span data-ttu-id="ca974-107">[Программа Microsoft 365 для обеспечения соответствия приложений](./application-certification.md)— это три уровня подходов к безопасности и соответствия требованиям приложений.</span><span class="sxs-lookup"><span data-stu-id="ca974-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="ca974-108">Каждый уровень строится на следующем – получив многослойную программу для удовлетворения потребностей клиента.</span><span class="sxs-lookup"><span data-stu-id="ca974-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="ca974-109">Чтобы узнать больше о безопасности и обеспечении соответствия требованиям для приложений Teams, посетите [страницу соответствие требованиям](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span><span class="sxs-lookup"><span data-stu-id="ca974-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="ca974-110">Добавление кнопки "Скачать" на сайт продукта</span><span class="sxs-lookup"><span data-stu-id="ca974-110">Add a download button to your product site</span></span>

<span data-ttu-id="ca974-111">Если ваше приложение находится в магазине Microsoft Teams, вы можете создать ссылку на ваш веб-сайт, на котором запускаются Teams и открыть диалоговое окно согласия и установки для пользователей, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="ca974-111">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="ca974-112">Формат: `https://teams.microsoft.com/l/app/<appId>` где AppID — это идентификатор GUID, который они объявляют в отправленном манифесте.</span><span class="sxs-lookup"><span data-stu-id="ca974-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="ca974-113">Пример: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` ссылка для установки Trello.</span><span class="sxs-lookup"><span data-stu-id="ca974-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="ca974-114">Обновление существующих приложений Teams</span><span class="sxs-lookup"><span data-stu-id="ca974-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="ca974-115">Не используйте кнопку *Добавить новое приложение* для повторной отсылки приложения.</span><span class="sxs-lookup"><span data-stu-id="ca974-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="ca974-116">Вместо этого используйте плитку для своего приложения на вкладке Обзор.</span><span class="sxs-lookup"><span data-stu-id="ca974-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="ca974-117">AppId в обновленном манифесте должно быть таким же, как и в текущем манифесте, с увеличенным номером версии.</span><span class="sxs-lookup"><span data-stu-id="ca974-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="ca974-118">Увеличьте номер версии в манифесте, если вы вносите изменения в манифест отправку.</span><span class="sxs-lookup"><span data-stu-id="ca974-118">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="ca974-119">Обновленные отправки необходимы для выполнения новой проверки и проверки.</span><span class="sxs-lookup"><span data-stu-id="ca974-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="ca974-120">Обновления приложения и процесс согласия пользователя</span><span class="sxs-lookup"><span data-stu-id="ca974-120">App updates and the user consent flow</span></span>

<span data-ttu-id="ca974-121">Когда пользователь устанавливает приложение, вы можете предоставить приложению разрешение на доступ к службам и сведениям, которые необходимы приложению для выполнения своей задачи.</span><span class="sxs-lookup"><span data-stu-id="ca974-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="ca974-122">В большинстве случаев после завершения обновления приложения будет автоматически отображаться новая версия для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="ca974-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="ca974-123">Однако существует несколько обновлений [манифеста приложения Teams](../../../../resources/schema/manifest-schema.md) , для выполнения которых требуется принятие пользователя и который может повторно активировать это поведение.</span><span class="sxs-lookup"><span data-stu-id="ca974-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="ca974-124">Добавлен или удален Bot.</span><span class="sxs-lookup"><span data-stu-id="ca974-124">A bot was added or removed.</span></span>
> * <span data-ttu-id="ca974-125">Изменено существующее уникальное значение для Bot `botId` .</span><span class="sxs-lookup"><span data-stu-id="ca974-125">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="ca974-126">`isNotificationOnly`Изменилось логическое значение существующего экземпляра Bot.</span><span class="sxs-lookup"><span data-stu-id="ca974-126">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="ca974-127">`supportsFiles`Изменилось логическое значение существующего экземпляра Bot.</span><span class="sxs-lookup"><span data-stu-id="ca974-127">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="ca974-128">Добавлено или удалено расширение обмена сообщениями ( `composeExtensions` ).</span><span class="sxs-lookup"><span data-stu-id="ca974-128">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="ca974-129">Добавлен новый соединитель.</span><span class="sxs-lookup"><span data-stu-id="ca974-129">A new connector was added.</span></span>
> * <span data-ttu-id="ca974-130">Добавлена новая вкладка "статический/личное".</span><span class="sxs-lookup"><span data-stu-id="ca974-130">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="ca974-131">Добавлена новая вкладка "Настраиваемая группа/канал".</span><span class="sxs-lookup"><span data-stu-id="ca974-131">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="ca974-132">`webApplicationInfo`Измененные значения.</span><span class="sxs-lookup"><span data-stu-id="ca974-132">The `webApplicationInfo` values changed.</span></span>
>
