---
title: Публикация после публикации
description: Что делать после публикации приложения
keywords: сертификат обновления публикаций после публикации Teams
ms.openlocfilehash: 77b74d77546de0ae93b0ae39aec925d2e3dec2cf
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867098"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="9b8b6-104">Обслуживание и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="9b8b6-104">Maintain and support your published app</span></span> 

<span data-ttu-id="9b8b6-105">После утверждения приложения и добавления его в список общедоступных каталогов приложений вы можете увеличить уровень доступности, добавив сертификат приложения или нажав кнопку скачать на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-105">After your app is approved and listed in the public app catalog, you can increase your reach by achieving app certification, or adding a download button your website.</span></span>

## <a name="application-certificate"></a><span data-ttu-id="9b8b6-106">Сертификат приложения</span><span class="sxs-lookup"><span data-stu-id="9b8b6-106">Application Certificate</span></span>

<span data-ttu-id="9b8b6-107">Корпорация Майкрософт предоставляет [программу для сертификации приложений](./application-certification.md) , которая компилирует сведения о приложении и представляет их на [странице безопасности и соответствия требованиям приложений Microsoft Teams](https://aka.ms/AppCertification).</span><span class="sxs-lookup"><span data-stu-id="9b8b6-107">Microsoft provides a [Application Certification program](./application-certification.md) that compiles your app information and presents it on [Microsoft Teams App Security and Compliance Page](https://aka.ms/AppCertification).</span></span> <span data-ttu-id="9b8b6-108">Эта информация предназначена для того, чтобы помочь администраторам выбрать приложения, которые являются безопасными для своих организаций.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-108">This information is intended to help admins to choose apps that are safe for their organizations.</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="9b8b6-109">Добавление кнопки "Скачать" на сайт продукта</span><span class="sxs-lookup"><span data-stu-id="9b8b6-109">Add a download button to your product site</span></span>

<span data-ttu-id="9b8b6-110">Если ваше приложение находится в магазине Microsoft Teams, вы можете создать ссылку на ваш веб-сайт, на котором запускаются Teams и открыть диалоговое окно согласия и установки для пользователей, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-110">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="9b8b6-111">Формат: `https://teams.microsoft.com/l/app/<appId>` где AppID — это идентификатор GUID, который они объявляют в отправленном манифесте.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-111">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="9b8b6-112">Пример: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` ссылка для установки Trello.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-112">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="9b8b6-113">Обновление существующих приложений Teams</span><span class="sxs-lookup"><span data-stu-id="9b8b6-113">Updating your existing Teams app</span></span>

* <span data-ttu-id="9b8b6-114">Не используйте кнопку *Добавить новое приложение* для повторной отсылки приложения.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-114">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="9b8b6-115">Вместо этого используйте плитку для своего приложения на вкладке Обзор.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-115">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="9b8b6-116">AppId в обновленном манифесте должно быть таким же, как и в текущем манифесте, с увеличенным номером версии.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-116">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="9b8b6-117">Увеличьте номер версии в манифесте, если вы вносите изменения в манифест отправку.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-117">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="9b8b6-118">Обновленные отправки необходимы для выполнения новой проверки и проверки.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-118">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="9b8b6-119">Обновления приложения и процесс согласия пользователя</span><span class="sxs-lookup"><span data-stu-id="9b8b6-119">App updates and the user consent flow</span></span>

<span data-ttu-id="9b8b6-120">Когда пользователь устанавливает приложение, вы можете предоставить приложению разрешение на доступ к службам и сведениям, которые необходимы приложению для выполнения своей задачи.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-120">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="9b8b6-121">В большинстве случаев после завершения обновления приложения будет автоматически отображаться новая версия для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-121">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="9b8b6-122">Однако существует несколько обновлений [манифеста приложения Teams](../../../../resources/schema/manifest-schema.md) , для выполнения которых требуется принятие пользователя и который может повторно активировать это поведение.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-122">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="9b8b6-123">Добавлен или удален Bot.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-123">A bot was added or removed.</span></span>
> * <span data-ttu-id="9b8b6-124">Изменено существующее уникальное значение для Bot `botId` .</span><span class="sxs-lookup"><span data-stu-id="9b8b6-124">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="9b8b6-125">`isNotificationOnly`Изменилось логическое значение существующего экземпляра Bot.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-125">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="9b8b6-126">`supportsFiles`Изменилось логическое значение существующего экземпляра Bot.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-126">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="9b8b6-127">Добавлено или удалено расширение обмена сообщениями ( `composeExtensions` ).</span><span class="sxs-lookup"><span data-stu-id="9b8b6-127">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="9b8b6-128">Добавлен новый соединитель.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-128">A new connector was added.</span></span>
> * <span data-ttu-id="9b8b6-129">Добавлена новая вкладка "статический/личное".</span><span class="sxs-lookup"><span data-stu-id="9b8b6-129">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="9b8b6-130">Добавлена новая вкладка "Настраиваемая группа/канал".</span><span class="sxs-lookup"><span data-stu-id="9b8b6-130">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="9b8b6-131">`webApplicationInfo`Измененные значения.</span><span class="sxs-lookup"><span data-stu-id="9b8b6-131">The `webApplicationInfo` values changed.</span></span>
>