---
title: Получение всех сообщений канала с помощью RSC
author: surbhigupta12
description: Получение всех сообщений канала с разрешениями RSC
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 833bdbc015cf852fcd899ce4e75f742448b89978
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631414"
---
# <a name="receive-all-channel-messages-with-rsc"></a><span data-ttu-id="a3727-103">Получение всех сообщений канала с помощью RSC</span><span class="sxs-lookup"><span data-stu-id="a3727-103">Receive all channel messages with RSC</span></span>

> [!NOTE]
> <span data-ttu-id="a3727-104">В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../../../resources/dev-preview/developer-preview-intro.md) разработчиков.</span><span class="sxs-lookup"><span data-stu-id="a3727-104">This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="a3727-105">Модель разрешений для разрешений для определенных ресурсов (RSC), изначально разработанная для Teams Graph API, теперь распространяется на сценарии ботов.</span><span class="sxs-lookup"><span data-stu-id="a3727-105">The resource-specific consent (RSC) permissions model, originally developed for Teams Graph APIs, is now extended to bot scenarios.</span></span>

<span data-ttu-id="a3727-106">В настоящее время боты могут получать сообщения каналов пользователей только при @mentioned.</span><span class="sxs-lookup"><span data-stu-id="a3727-106">Currently, bots can only receive user channel messages when they are @mentioned.</span></span> <span data-ttu-id="a3727-107">Теперь с помощью RSC можно запрашивать у владельцев команд согласие на получение ботом сообщений пользователей по стандартным каналам в команде без @mentioned.</span><span class="sxs-lookup"><span data-stu-id="a3727-107">Using RSC, you can now request team owners to consent for a bot to receive user messages across standard channels in a team without being @mentioned.</span></span> <span data-ttu-id="a3727-108">Эта возможность включена, указав разрешение в манифесте включенного `ChannelMessage.Read.Group` приложения RSC Teams.</span><span class="sxs-lookup"><span data-stu-id="a3727-108">This capability is enabled by specifying the `ChannelMessage.Read.Group` permission in the manifest of an RSC enabled Teams app.</span></span> <span data-ttu-id="a3727-109">После настройки владельцы команд могут предоставить согласие во время процесса установки приложения.</span><span class="sxs-lookup"><span data-stu-id="a3727-109">After configuration, team owners can grant consent during the app installation process.</span></span>

<span data-ttu-id="a3727-110">Дополнительные сведения о включаемом RSC для вашего [приложения](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)см. в Teams.</span><span class="sxs-lookup"><span data-stu-id="a3727-110">For more information about enabling RSC for your app, see [resource-specific consent in Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).</span></span>

## <a name="enable-bots-to-receive-all-channel-messages"></a><span data-ttu-id="a3727-111">Включить боты для получения всех сообщений канала</span><span class="sxs-lookup"><span data-stu-id="a3727-111">Enable bots to receive all channel messages</span></span>

<span data-ttu-id="a3727-112">Разрешение `ChannelMessage.Read.Group` RSC распространяется на ботов.</span><span class="sxs-lookup"><span data-stu-id="a3727-112">The `ChannelMessage.Read.Group` RSC permission is extended to bots.</span></span> <span data-ttu-id="a3727-113">С согласия пользователя это разрешение позволяет приложениям графиков получать все сообщения в беседе, а боты получают все сообщения канала без @mentioned.</span><span class="sxs-lookup"><span data-stu-id="a3727-113">With user consent, this permission allows graph applications to get all messages in a conversation and bots to receive all channel messages without being @mentioned.</span></span>

## <a name="update-app-manifest"></a><span data-ttu-id="a3727-114">Манифест обновления приложения</span><span class="sxs-lookup"><span data-stu-id="a3727-114">Update app manifest</span></span>

<span data-ttu-id="a3727-115">Чтобы бот получал все сообщения канала, RSC должен быть настроен в манифесте приложения Teams с разрешения, указанного `ChannelMessage.Read.Group` в `webApplicationInfo` свойстве.</span><span class="sxs-lookup"><span data-stu-id="a3727-115">For your bot to receive all channel messages, RSC must be configured in the Teams app manifest with the `ChannelMessage.Read.Group` permission specified in the `webApplicationInfo` property.</span></span>

![Манифест обновления приложения](~/bots/how-to/conversations/Media/appmanifest.png)

<span data-ttu-id="a3727-117">Ниже приводится пример `webApplicationInfo` объекта:</span><span class="sxs-lookup"><span data-stu-id="a3727-117">The following is an example of the `webApplicationInfo` object:</span></span>

* <span data-ttu-id="a3727-118">**id:** ID Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="a3727-118">**id**: Your Azure Active Directory (AAD) app ID.</span></span> <span data-ttu-id="a3727-119">Это может быть то же самое, что и ваш бот-ИД.</span><span class="sxs-lookup"><span data-stu-id="a3727-119">This can be the same as your bot ID.</span></span>
* <span data-ttu-id="a3727-120">**ресурс.** Любая строка.</span><span class="sxs-lookup"><span data-stu-id="a3727-120">**resource**: Any string.</span></span> <span data-ttu-id="a3727-121">Это поле не имеет операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа на ошибки.</span><span class="sxs-lookup"><span data-stu-id="a3727-121">This field has no operation in RSC, but must be added and have a value to avoid error response.</span></span>
* <span data-ttu-id="a3727-122">**applicationPermissions:** разрешения RSC для вашего приложения с `ChannelMessage.Read.Group` должны быть указаны.</span><span class="sxs-lookup"><span data-stu-id="a3727-122">**applicationPermissions**: RSC permissions for your app with `ChannelMessage.Read.Group` must be specified.</span></span> <span data-ttu-id="a3727-123">Дополнительные сведения см. [в ресурсных разрешениях.](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="a3727-123">For more information, see [resource-specific permissions](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).</span></span>

<span data-ttu-id="a3727-124">В следующем коде приводится пример манифеста приложения:</span><span class="sxs-lookup"><span data-stu-id="a3727-124">The following code provides an example of the app manifest:</span></span>

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team-to-test"></a><span data-ttu-id="a3727-125">Sideload in a team to test</span><span class="sxs-lookup"><span data-stu-id="a3727-125">Sideload in a team to test</span></span>

<span data-ttu-id="a3727-126">Чтобы проверить, получаются ли все сообщения канала в команде с RSC без @mentioned:</span><span class="sxs-lookup"><span data-stu-id="a3727-126">To sideload in a team to test, whether all channel messages in a team with RSC are received without being @mentioned:</span></span>

1. <span data-ttu-id="a3727-127">Выберите или создайте команду.</span><span class="sxs-lookup"><span data-stu-id="a3727-127">Select or create a team.</span></span>
1. <span data-ttu-id="a3727-128">Выберите эллипсы &#x25CF;&#x25CF;&#x25CF; левой области.</span><span class="sxs-lookup"><span data-stu-id="a3727-128">Select the ellipses &#x25CF;&#x25CF;&#x25CF; from the left pane.</span></span> <span data-ttu-id="a3727-129">Отображается выпадаемое меню.</span><span class="sxs-lookup"><span data-stu-id="a3727-129">The drop-down menu appears.</span></span>
1. <span data-ttu-id="a3727-130">Выберите **команду Manage** из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="a3727-130">Select **Manage team** from the drop-down menu.</span></span> <span data-ttu-id="a3727-131">Сведения отображаются.</span><span class="sxs-lookup"><span data-stu-id="a3727-131">The details appear.</span></span>

   ![Управление приложениями в команде](~/bots/how-to/conversations/Media/managingteam.png)

1. <span data-ttu-id="a3727-133">Выберите **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="a3727-133">Select **Apps**.</span></span> <span data-ttu-id="a3727-134">Отображаются несколько приложений.</span><span class="sxs-lookup"><span data-stu-id="a3727-134">Multiple apps appear.</span></span>
1. <span data-ttu-id="a3727-135">Выберите **Upload настраиваемого приложения из** нижнего правого угла.</span><span class="sxs-lookup"><span data-stu-id="a3727-135">Select **Upload a custom app** from the lower right corner.</span></span>

    ![Загрузка настраиваемой приложения](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. <span data-ttu-id="a3727-137">Выберите пакет приложения из **открытого** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a3727-137">Select the app package from the **Open** dialog box.</span></span>
1. <span data-ttu-id="a3727-138">Выберите **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="a3727-138">Select **Open**.</span></span>

    ![Выбор пакета приложений](~/bots/how-to/conversations/Media/selectapppackage.png)

1. <span data-ttu-id="a3727-140">Выберите **Добавить** из всплывающее всплывающее приложение сведений о приложении, чтобы добавить бот в выбранную команду.</span><span class="sxs-lookup"><span data-stu-id="a3727-140">Select **Add** from the app details pop-up, to add the bot to your selected team.</span></span>

    ![Добавление бота](~/bots/how-to/conversations/Media/addingbot.png)

1. <span data-ttu-id="a3727-142">Выберите канал и введите сообщение в канале для бота.</span><span class="sxs-lookup"><span data-stu-id="a3727-142">Select a channel and enter a message in the channel for your bot.</span></span>

    <span data-ttu-id="a3727-143">Бот получает сообщение, не будучи @mentioned.</span><span class="sxs-lookup"><span data-stu-id="a3727-143">The bot receives the message without being @mentioned.</span></span>

    ![Бот получает сообщение](~/bots/how-to/conversations/Media/botreceivingmessage.png)

## <a name="see-also"></a><span data-ttu-id="a3727-145">См. также</span><span class="sxs-lookup"><span data-stu-id="a3727-145">See also</span></span>

* [<span data-ttu-id="a3727-146">Беседы с ботами</span><span class="sxs-lookup"><span data-stu-id="a3727-146">Bot conversations</span></span>](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [<span data-ttu-id="a3727-147">Согласие для определенных ресурсов</span><span class="sxs-lookup"><span data-stu-id="a3727-147">Resource-specific consent</span></span>](/microsoftteams/resource-specific-consent)
* [<span data-ttu-id="a3727-148">Проверка согласия на конкретные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a3727-148">Test resource-specific consent</span></span>](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [<span data-ttu-id="a3727-149">Upload настраиваемом приложении в Teams</span><span class="sxs-lookup"><span data-stu-id="a3727-149">Upload custom app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
