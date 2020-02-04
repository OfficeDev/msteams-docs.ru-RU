---
title: Публикация после публикации
description: Что делать после публикации приложения
keywords: сертификат обновления публикаций после публикации Teams
ms.openlocfilehash: 05e4ea47bbf81967ccf086230bf0ad8c633f6e0b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675262"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="63aa6-104">Обслуживание и поддержка опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="63aa6-104">Maintain and support your published app</span></span> 

<span data-ttu-id="63aa6-105">После утверждения приложения и добавления его в список общедоступных каталогов приложений вы можете увеличить уровень доступности, добавив сертификат приложения или нажав кнопку скачать на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="63aa6-105">After your app is approved and listed in the public app catalog, you can increase your reach by achieving app certification, or adding a download button your website.</span></span>

## <a name="application-certificate"></a><span data-ttu-id="63aa6-106">Сертификат приложения</span><span class="sxs-lookup"><span data-stu-id="63aa6-106">Application Certificate</span></span>

<span data-ttu-id="63aa6-107">Корпорация Майкрософт предоставляет [программу для сертификации приложений](./application-certification.md) , которая компилирует сведения о приложении и представляет их на [странице безопасности и соответствия требованиям приложений Microsoft Teams](https://aka.ms/AppCertification).</span><span class="sxs-lookup"><span data-stu-id="63aa6-107">Microsoft provides a [Application Certification program](./application-certification.md) that compiles your app information and presents it on [Microsoft Teams App Security and Compliance Page](https://aka.ms/AppCertification).</span></span> <span data-ttu-id="63aa6-108">Эта информация предназначена для того, чтобы помочь администраторам выбрать приложения, которые являются безопасными для своих организаций.</span><span class="sxs-lookup"><span data-stu-id="63aa6-108">This information is intended to help admins to choose apps that are safe for their organizations.</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="63aa6-109">Добавление кнопки "Скачать" на сайт продукта</span><span class="sxs-lookup"><span data-stu-id="63aa6-109">Add a download button to your product site</span></span>

<span data-ttu-id="63aa6-110">Если ваше приложение находится в магазине Microsoft Teams, вы можете создать ссылку на ваш веб-сайт, на котором запускаются Teams и открыть диалоговое окно согласия и установки для пользователей, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="63aa6-110">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="63aa6-111">Формат: `https://teams.microsoft.com/l/app/<appId>` где AppID — это идентификатор GUID, который они объявляют в отправленном манифесте.</span><span class="sxs-lookup"><span data-stu-id="63aa6-111">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="63aa6-112">Пример: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` ссылка для установки Trello.</span><span class="sxs-lookup"><span data-stu-id="63aa6-112">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="63aa6-113">Обновление существующих приложений Teams</span><span class="sxs-lookup"><span data-stu-id="63aa6-113">Updating your existing Teams app</span></span>

* <span data-ttu-id="63aa6-114">Не используйте кнопку *Добавить новое приложение* для повторной отсылки приложения.</span><span class="sxs-lookup"><span data-stu-id="63aa6-114">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="63aa6-115">Вместо этого используйте плитку для своего приложения на вкладке Обзор.</span><span class="sxs-lookup"><span data-stu-id="63aa6-115">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="63aa6-116">AppId в обновленном манифесте должно быть таким же, как и в текущем манифесте, с увеличенным номером версии.</span><span class="sxs-lookup"><span data-stu-id="63aa6-116">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="63aa6-117">Увеличьте номер версии в манифесте.</span><span class="sxs-lookup"><span data-stu-id="63aa6-117">Increment your version number in your manifest.</span></span>

### <a name="when-does-updating-your-app-trigger-the-user-consent-flow"></a><span data-ttu-id="63aa6-118">При обновлении приложения вызывается ли процесс согласия пользователя?</span><span class="sxs-lookup"><span data-stu-id="63aa6-118">When does updating your app trigger the user consent flow?</span></span>

<span data-ttu-id="63aa6-119">Когда пользователь устанавливает приложение, вы можете предоставить приложению разрешение на доступ к службам и сведениям, которые необходимы приложению для выполнения своей задачи.</span><span class="sxs-lookup"><span data-stu-id="63aa6-119">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="63aa6-120">При обновлении приложения это может привести к повторному срабатыванию этого поведения, особенно если вы внесли одно или несколько из следующих изменений:</span><span class="sxs-lookup"><span data-stu-id="63aa6-120">When you update your app, that can re-trigger this consent behavior, particularly if you have made one or more of the following changes:</span></span>

* <span data-ttu-id="63aa6-121">Добавление новой возможности в приложение, например добавление элемента Bot в приложение с вкладками.</span><span class="sxs-lookup"><span data-stu-id="63aa6-121">Adding a new capability to an app such as adding a bot to an tab only app.</span></span>
* <span data-ttu-id="63aa6-122">Изменение массива разрешений в манифесте.</span><span class="sxs-lookup"><span data-stu-id="63aa6-122">Changing the permissions array in the manifest.</span></span>
* <span data-ttu-id="63aa6-123">Увеличьте номер версии приложения в манифесте.</span><span class="sxs-lookup"><span data-stu-id="63aa6-123">Increment your app version number in your manifest.</span></span>
