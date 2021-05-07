---
title: Настройка параметров установки по умолчанию для приложения
description: Описывает, как указать параметры установки приложения по умолчанию.
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 561a4f2910e703db5ffce6176f6177dfd661d2ce
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230934"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a><span data-ttu-id="14af2-103">Настройка параметров установки по умолчанию для Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="14af2-103">Configure default install options for your Microsoft Teams app</span></span>

<span data-ttu-id="14af2-104">Обычно приложение поддерживает несколько сценариев в Teams, но вы, возможно, разработали его с учетом определенных областей и возможностей.</span><span class="sxs-lookup"><span data-stu-id="14af2-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="14af2-105">Например, если приложение предназначено в основном для использования в команде или канале, вы можете убедиться, что первый параметр установки, который пользователи видят в магазине, это **Добавление в команду.**</span><span class="sxs-lookup"><span data-stu-id="14af2-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

:::row:::
   :::column span="2":::

![Добавление примера отсевов приложений](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

<span data-ttu-id="14af2-107">Если основными возможностями вашего приложения является бот, вы также можете сделать ботом возможность по умолчанию, когда пользователь устанавливает приложение в команду.</span><span class="sxs-lookup"><span data-stu-id="14af2-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span>

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="14af2-108">Настройка области установки приложения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="14af2-108">Configure your app's default install scope</span></span>

<span data-ttu-id="14af2-109">Настройка области установки по умолчанию для приложения.</span><span class="sxs-lookup"><span data-stu-id="14af2-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="14af2-110">За один раз можно установить только одну область.</span><span class="sxs-lookup"><span data-stu-id="14af2-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="14af2-111">**Настройка области установки по умолчанию в манифесте приложения**</span><span class="sxs-lookup"><span data-stu-id="14af2-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="14af2-112">Откройте манифест приложения и добавьте `defaultInstallScope` свойство.</span><span class="sxs-lookup"><span data-stu-id="14af2-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="14af2-113">Установите значение области установки по умолчанию как `personal` , или , или `team` `groupchat` `meetings` .</span><span class="sxs-lookup"><span data-stu-id="14af2-113">Set default install scope value as, either `personal`, `team`, `groupchat`, or `meetings`.</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="14af2-114">Дополнительные сведения см. в [схеме манифеста приложения.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="14af2-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="14af2-115">Настройка возможностей по умолчанию для общих областей</span><span class="sxs-lookup"><span data-stu-id="14af2-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="14af2-116">Настройка возможностей по умолчанию при установке приложения для группы, собрания или группового чата.</span><span class="sxs-lookup"><span data-stu-id="14af2-116">Configure the default capability when your app is installed for a team, meeting, or groupchat.</span></span>

> [!NOTE]
> <span data-ttu-id="14af2-117">`defaultGroupCapability` предоставляет возможности по умолчанию, которые будут добавлены в группу, групповой чат или собрание.</span><span class="sxs-lookup"><span data-stu-id="14af2-117">`defaultGroupCapability` provides the default capability that will be added to the team, groupchat, or meeting.</span></span> <span data-ttu-id="14af2-118">Выберите вкладку, бот или соединительщик в качестве возможности по умолчанию для приложения, но необходимо убедиться, что вы предоставили выбранную возможность в определении приложения.</span><span class="sxs-lookup"><span data-stu-id="14af2-118">Select a tab, bot, or connector as the default capability for your app, but you must ensure that you have provided the selected capability in your app definition.</span></span>

<span data-ttu-id="14af2-119">**Настройка сведений в манифесте приложения**</span><span class="sxs-lookup"><span data-stu-id="14af2-119">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="14af2-120">Откройте манифест приложения и добавьте `defaultGroupCapability` в него свойство.</span><span class="sxs-lookup"><span data-stu-id="14af2-120">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="14af2-121">Установите значение `team` , `groupchat` или `meetings` .</span><span class="sxs-lookup"><span data-stu-id="14af2-121">Set a value of `team`, `groupchat`, or `meetings`.</span></span>
3. <span data-ttu-id="14af2-122">Для выбранной возможности группы доступны групповые возможности, `bot` или `tab` `connector` .</span><span class="sxs-lookup"><span data-stu-id="14af2-122">For the selected group capability, the available group capabilities are, `bot`, `tab`, or `connector`.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="14af2-123">Вы можете выбрать только одну возможность по умолчанию или для выбранной `bot` `tab` `connector` группы.</span><span class="sxs-lookup"><span data-stu-id="14af2-123">You can select only one default capability, `bot`, `tab`, or `connector` for the selected group capability.</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> <span data-ttu-id="14af2-124">Дополнительные сведения см. в [схеме манифеста приложения.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="14af2-124">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="14af2-125">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="14af2-125">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="14af2-126">Создание пакета приложений</span><span class="sxs-lookup"><span data-stu-id="14af2-126">Create your app package</span></span>](~/concepts/build-and-test/apps-package.md)
