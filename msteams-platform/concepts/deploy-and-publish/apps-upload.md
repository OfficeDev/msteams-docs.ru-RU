---
title: Upload пользовательское приложение
description: Узнайте, как перезагрузить приложение в Microsoft Teams. Боковая загрузка является обычной при тестировании и отладке приложения во время разработки.
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 39e94317ceb615ecd7d5481276ffafed5afe5cde
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565195"
---
# <a name="upload-your-app-in-microsoft-teams"></a><span data-ttu-id="c40ed-104">Upload приложение в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c40ed-104">Upload your app in Microsoft Teams</span></span>

<span data-ttu-id="c40ed-105">Вы можете Microsoft Teams приложения без публикации в вашей организации или Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="c40ed-105">You can sideload Microsoft Teams apps without having to publish to your organization or the Teams store.</span></span> <span data-ttu-id="c40ed-106">Это имеет смысл в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="c40ed-106">This makes sense in the following scenarios:</span></span>

* <span data-ttu-id="c40ed-107">Вы хотите протестировать и отладить приложение локально самостоятельно или с другими разработчиками.</span><span class="sxs-lookup"><span data-stu-id="c40ed-107">You want to test and debug an app locally yourself or with other developers.</span></span>
* <span data-ttu-id="c40ed-108">Вы создали приложение только для себя.</span><span class="sxs-lookup"><span data-stu-id="c40ed-108">You built an app just for yourself.</span></span> <span data-ttu-id="c40ed-109">Например, автоматизировать рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="c40ed-109">For example, to automate a workflow.</span></span>
* <span data-ttu-id="c40ed-110">Вы создали приложение для небольшого набора пользователей, например рабочей группы.</span><span class="sxs-lookup"><span data-stu-id="c40ed-110">You built an app for a small set of users, such as, your work group.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c40ed-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c40ed-111">Prerequisites</span></span>

* <span data-ttu-id="c40ed-112">Создайте пакет [приложений и](~/concepts/build-and-test/apps-package.md) [проверяйте его на](https://dev.teams.microsoft.com/appvalidation.html) ошибки.</span><span class="sxs-lookup"><span data-stu-id="c40ed-112">Create your [app package](~/concepts/build-and-test/apps-package.md) and [validate it](https://dev.teams.microsoft.com/appvalidation.html) for errors.</span></span>
* <span data-ttu-id="c40ed-113">[Включите пользовательскую загрузку приложения](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) в Teams.</span><span class="sxs-lookup"><span data-stu-id="c40ed-113">[Enable custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) in Teams.</span></span>
* <span data-ttu-id="c40ed-114">Убедитесь, что ваше приложение работает и доступно через HTTPs.</span><span class="sxs-lookup"><span data-stu-id="c40ed-114">Make sure that your app is running and accessible via HTTPs.</span></span>

## <a name="upload-your-app"></a><span data-ttu-id="c40ed-115">Отправка пакета приложения</span><span class="sxs-lookup"><span data-stu-id="c40ed-115">Upload your app</span></span>

<span data-ttu-id="c40ed-116">Вы можете настроить приложение в группу, общаться, встречаться или для личного пользования в зависимости от того, как вы настроили область действия приложения.</span><span class="sxs-lookup"><span data-stu-id="c40ed-116">You can sideload your app to a team, chat, meeting, or for personal use depending on how you configured your app's scope.</span></span>

1. <span data-ttu-id="c40ed-117">Войдите в систему к Teams с вашей [учетной Microsoft 365 развития.](~/build-your-first-app/build-and-run.md#prerequisites)</span><span class="sxs-lookup"><span data-stu-id="c40ed-117">Log in to the Teams client with your [Microsoft 365 development account](~/build-your-first-app/build-and-run.md#prerequisites).</span></span>
1. <span data-ttu-id="c40ed-118">Выберите **приложения** и **выберите Upload пользовательское приложение.**</span><span class="sxs-lookup"><span data-stu-id="c40ed-118">Select **Apps** and choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="c40ed-119">Выберите пакет приложений .zip файл.</span><span class="sxs-lookup"><span data-stu-id="c40ed-119">Select your app package .zip file.</span></span> <span data-ttu-id="c40ed-120">Установка диалоговых дисплеев.</span><span class="sxs-lookup"><span data-stu-id="c40ed-120">An install dialog displays.</span></span>
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Скриншот, показывающий пример Teams установки диалога.":::
1. <span data-ttu-id="c40ed-122">Добавьте приложение в Teams.</span><span class="sxs-lookup"><span data-stu-id="c40ed-122">Add your app to Teams.</span></span>

## <a name="troubleshoot-upload-issues"></a><span data-ttu-id="c40ed-123">Устранение неполадок при отправке</span><span class="sxs-lookup"><span data-stu-id="c40ed-123">Troubleshoot upload issues</span></span>

<span data-ttu-id="c40ed-124">Если ваше приложение не может перегрузиться, сделайте следующее до тех пор, пока проблема не решится:</span><span class="sxs-lookup"><span data-stu-id="c40ed-124">If your app fails to sideload, do the following until the issue resolves:</span></span>

1. <span data-ttu-id="c40ed-125">Вернитесь через инструкции [по созданию пакета приложений.](../../concepts/build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="c40ed-125">Go back through the instructions for [creating your app package](../../concepts/build-and-test/apps-package.md).</span></span>
1. <span data-ttu-id="c40ed-126">[Еще раз проиймите](https://dev.teams.microsoft.com/appvalidation.html) пакет приложений.</span><span class="sxs-lookup"><span data-stu-id="c40ed-126">[Validate your app package](https://dev.teams.microsoft.com/appvalidation.html) again.</span></span>
1. <span data-ttu-id="c40ed-127">Убедитесь, что манифест приложения соответствует [последней схеме.](../../resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="c40ed-127">Make sure your app manifest matches the latest [schema](../../resources/schema/manifest-schema.md).</span></span>

## <a name="access-your-app"></a><span data-ttu-id="c40ed-128">Доступ к приложению</span><span class="sxs-lookup"><span data-stu-id="c40ed-128">Access your app</span></span>

<span data-ttu-id="c40ed-129">Teams предоставляет несколько способов открытия приложений.</span><span class="sxs-lookup"><span data-stu-id="c40ed-129">Teams provides several ways to open apps.</span></span> <span data-ttu-id="c40ed-130">Для получения дополнительной информации [смотрите доступ к приложениям в Teams.](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)</span><span class="sxs-lookup"><span data-stu-id="c40ed-130">For more information, see [access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span></span>

## <a name="update-your-app"></a><span data-ttu-id="c40ed-131">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="c40ed-131">Update your app</span></span>

<span data-ttu-id="c40ed-132">Вам больше не нужно снова входить в приложение, если вы внести изменения в код (они отражены в Teams в режиме реального времени).</span><span class="sxs-lookup"><span data-stu-id="c40ed-132">You don't have to sideload your app again if you make code changes (these are reflected in Teams in real-time).</span></span> <span data-ttu-id="c40ed-133">Однако необходимо переустановить настройки, если вы измените конфигурацию приложения.</span><span class="sxs-lookup"><span data-stu-id="c40ed-133">However, you must reinstall if you change any app configurations.</span></span>

## <a name="remove-your-app"></a><span data-ttu-id="c40ed-134">Удалить приложение</span><span class="sxs-lookup"><span data-stu-id="c40ed-134">Remove your app</span></span>

<span data-ttu-id="c40ed-135">Чтобы удалить приложение, нажмите на значок приложения в Teams и **выберите Uninstall.**</span><span class="sxs-lookup"><span data-stu-id="c40ed-135">To remove your app, right click the app icon in Teams and select **Uninstall**.</span></span>

> [!NOTE]
> <span data-ttu-id="c40ed-136">Вы не можете удалить личную активность бота полностью.</span><span class="sxs-lookup"><span data-stu-id="c40ed-136">You can't remove personal bot activity entirely.</span></span> <span data-ttu-id="c40ed-137">Если вы удалите приложение и добавите его снова, новая связь с ботом пристройки к предыдущему разговору с ним.</span><span class="sxs-lookup"><span data-stu-id="c40ed-137">If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.</span></span>

## <a name="next-step"></a><span data-ttu-id="c40ed-138">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="c40ed-138">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c40ed-139">Используйте свое Teams приложение</span><span class="sxs-lookup"><span data-stu-id="c40ed-139">Use your Teams app</span></span>](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
