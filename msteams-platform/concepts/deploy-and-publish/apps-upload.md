---
title: Upload настраиваемом приложении
description: Узнайте, как перегрузить приложение в Microsoft Teams. При тестировании и отладке приложения во время разработки часто используется боковая загрузка.
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: a54068ffd57a5d622cad72267c049cee69b18d58
ms.sourcegitcommit: 2c8b35899dd845acd66f1f927e40d99523c29a91
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2021
ms.locfileid: "52684651"
---
# <a name="upload-your-app-in-microsoft-teams"></a><span data-ttu-id="9fde8-104">Upload приложение в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9fde8-104">Upload your app in Microsoft Teams</span></span>

<span data-ttu-id="9fde8-105">Вы можете Microsoft Teams приложения без публикации в организации или Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="9fde8-105">You can sideload Microsoft Teams apps without having to publish to your organization or the Teams store.</span></span> <span data-ttu-id="9fde8-106">Это имеет смысл в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="9fde8-106">This makes sense in the following scenarios:</span></span>

* <span data-ttu-id="9fde8-107">Вы хотите протестировать и отчудить приложение локально самостоятельно или с другими разработчиками.</span><span class="sxs-lookup"><span data-stu-id="9fde8-107">You want to test and debug an app locally yourself or with other developers.</span></span>
* <span data-ttu-id="9fde8-108">Вы создали приложение только для себя.</span><span class="sxs-lookup"><span data-stu-id="9fde8-108">You built an app just for yourself.</span></span> <span data-ttu-id="9fde8-109">Например, автоматизировать рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="9fde8-109">For example, to automate a workflow.</span></span>
* <span data-ttu-id="9fde8-110">Вы создали приложение для небольшого набора пользователей, например рабочей группы.</span><span class="sxs-lookup"><span data-stu-id="9fde8-110">You built an app for a small set of users, such as, your work group.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fde8-111">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="9fde8-111">Prerequisites</span></span>

* <span data-ttu-id="9fde8-112">Создайте [пакет приложения](~/concepts/build-and-test/apps-package.md) и проверьте его [на](https://dev.teams.microsoft.com/appvalidation.html) ошибки.</span><span class="sxs-lookup"><span data-stu-id="9fde8-112">Create your [app package](~/concepts/build-and-test/apps-package.md) and [validate it](https://dev.teams.microsoft.com/appvalidation.html) for errors.</span></span>
* <span data-ttu-id="9fde8-113">[Включить настраиваемую загрузку](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="9fde8-113">[Enable custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) in Teams.</span></span>
* <span data-ttu-id="9fde8-114">Убедитесь, что ваше приложение работает и доступно с помощью HTTP.</span><span class="sxs-lookup"><span data-stu-id="9fde8-114">Make sure that your app is running and accessible via HTTPs.</span></span>

## <a name="upload-your-app"></a><span data-ttu-id="9fde8-115">Отправка пакета приложения</span><span class="sxs-lookup"><span data-stu-id="9fde8-115">Upload your app</span></span>

<span data-ttu-id="9fde8-116">Вы можете перегрузить приложение в команду, чат, собрание или для личного использования в зависимости от настройки области приложения.</span><span class="sxs-lookup"><span data-stu-id="9fde8-116">You can sideload your app to a team, chat, meeting, or for personal use depending on how you configured your app's scope.</span></span>

1. <span data-ttu-id="9fde8-117">Войдите в Teams клиент с Microsoft 365 [учетной записью разработки.](~/build-your-first-app/build-and-run.md#prerequisites)</span><span class="sxs-lookup"><span data-stu-id="9fde8-117">Log in to the Teams client with your [Microsoft 365 development account](~/build-your-first-app/build-and-run.md#prerequisites).</span></span>
1. <span data-ttu-id="9fde8-118">Выберите **Приложения** и **выберите Upload настраиваемом приложении.**</span><span class="sxs-lookup"><span data-stu-id="9fde8-118">Select **Apps** and choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="9fde8-119">Выберите пакет приложений .zip файл.</span><span class="sxs-lookup"><span data-stu-id="9fde8-119">Select your app package .zip file.</span></span> <span data-ttu-id="9fde8-120">Отображает диалоговое окно установки.</span><span class="sxs-lookup"><span data-stu-id="9fde8-120">An install dialog displays.</span></span>
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Снимок экрана, показывающий пример диалогового Teams установки приложения.":::
1. <span data-ttu-id="9fde8-122">Добавьте приложение в Teams.</span><span class="sxs-lookup"><span data-stu-id="9fde8-122">Add your app to Teams.</span></span>

## <a name="troubleshoot-upload-issues"></a><span data-ttu-id="9fde8-123">Устранение неполадок при отправке</span><span class="sxs-lookup"><span data-stu-id="9fde8-123">Troubleshoot upload issues</span></span>

<span data-ttu-id="9fde8-124">Если приложение не перегрузит, сделайте следующее, пока проблема не решится:</span><span class="sxs-lookup"><span data-stu-id="9fde8-124">If your app fails to sideload, do the following until the issue resolves:</span></span>

1. <span data-ttu-id="9fde8-125">Возвращайся к инструкциям по созданию [пакета приложений.](../../concepts/build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="9fde8-125">Go back through the instructions for [creating your app package](../../concepts/build-and-test/apps-package.md).</span></span>
1. <span data-ttu-id="9fde8-126">[Проверка пакета приложений снова.](https://dev.teams.microsoft.com/appvalidation.html)</span><span class="sxs-lookup"><span data-stu-id="9fde8-126">[Validate your app package](https://dev.teams.microsoft.com/appvalidation.html) again.</span></span>
1. <span data-ttu-id="9fde8-127">Убедитесь, что манифест приложения соответствует последней [схеме.](../../resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="9fde8-127">Ensure your app manifest matches the latest [schema](../../resources/schema/manifest-schema.md).</span></span>

## <a name="access-your-app"></a><span data-ttu-id="9fde8-128">Доступ к приложению</span><span class="sxs-lookup"><span data-stu-id="9fde8-128">Access your app</span></span>

<span data-ttu-id="9fde8-129">Teams предоставляет несколько способов открытия приложений.</span><span class="sxs-lookup"><span data-stu-id="9fde8-129">Teams provides several ways to open apps.</span></span> <span data-ttu-id="9fde8-130">Дополнительные сведения см. [в Teams.](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)</span><span class="sxs-lookup"><span data-stu-id="9fde8-130">For more information, see [access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span></span>

## <a name="update-your-app"></a><span data-ttu-id="9fde8-131">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="9fde8-131">Update your app</span></span>

<span data-ttu-id="9fde8-132">При внесении изменений кода (они отражаются в Teams в режиме реального времени) не нужно снова перегружать приложение.</span><span class="sxs-lookup"><span data-stu-id="9fde8-132">You don't have to sideload your app again if you make code changes (these are reflected in Teams in real-time).</span></span> <span data-ttu-id="9fde8-133">Однако при изменении конфигураций приложений необходимо переустановить.</span><span class="sxs-lookup"><span data-stu-id="9fde8-133">However, you must reinstall if you change any app configurations.</span></span>

## <a name="remove-your-app"></a><span data-ttu-id="9fde8-134">Удаление приложения</span><span class="sxs-lookup"><span data-stu-id="9fde8-134">Remove your app</span></span>

<span data-ttu-id="9fde8-135">Чтобы удалить приложение, нажмите правой кнопкой мыши значок приложения в Teams и выберите **Uninstall**.</span><span class="sxs-lookup"><span data-stu-id="9fde8-135">To remove your app, right click the app icon in Teams and select **Uninstall**.</span></span>

> [!NOTE]
> <span data-ttu-id="9fde8-136">Полностью удалить личную активность бота нельзя.</span><span class="sxs-lookup"><span data-stu-id="9fde8-136">You can't remove personal bot activity entirely.</span></span> <span data-ttu-id="9fde8-137">Если удалить приложение и добавить его еще раз, новое общение с ботом добавляется к предыдущему разговору с ним.</span><span class="sxs-lookup"><span data-stu-id="9fde8-137">If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.</span></span>

## <a name="next-step"></a><span data-ttu-id="9fde8-138">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="9fde8-138">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9fde8-139">Используйте приложение Teams</span><span class="sxs-lookup"><span data-stu-id="9fde8-139">Use your Teams app</span></span>](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
