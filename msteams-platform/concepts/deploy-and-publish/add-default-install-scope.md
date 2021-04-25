---
title: Настройка параметров установки по умолчанию для приложения
description: Описывает, как указать параметры установки приложения по умолчанию.
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a4b70df70c7b9442e29953dae8a8c4e892cb72c1
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946492"
---
# <a name="add-a-default-install-scope-and-group-capability"></a><span data-ttu-id="d48f4-103">Добавление области установки по умолчанию и возможности групповой установки</span><span class="sxs-lookup"><span data-stu-id="d48f4-103">Add a default install scope and group capability</span></span>

<span data-ttu-id="d48f4-104">Обычно приложение поддерживает несколько сценариев в Teams, но вы, возможно, разработали его с учетом определенных областей и возможностей.</span><span class="sxs-lookup"><span data-stu-id="d48f4-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="d48f4-105">Например, если приложение предназначено в основном для использования в команде или канале, вы можете убедиться, что первый параметр установки, который пользователи видят в магазине, это **Добавление в команду.**</span><span class="sxs-lookup"><span data-stu-id="d48f4-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

![Добавление приложения](../../assets/images/compose-extensions/addanapp.png)

<span data-ttu-id="d48f4-107">Если основными возможностями вашего приложения является бот, вы также можете сделать ботом возможность по умолчанию, когда пользователь устанавливает приложение в команду.</span><span class="sxs-lookup"><span data-stu-id="d48f4-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span> 

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="d48f4-108">Настройка области установки приложения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d48f4-108">Configure your app's default install scope</span></span>

<span data-ttu-id="d48f4-109">Настройка области установки по умолчанию для приложения.</span><span class="sxs-lookup"><span data-stu-id="d48f4-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="d48f4-110">За один раз можно установить только одну область.</span><span class="sxs-lookup"><span data-stu-id="d48f4-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="d48f4-111">**Настройка области установки по умолчанию в манифесте приложения**</span><span class="sxs-lookup"><span data-stu-id="d48f4-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="d48f4-112">Откройте манифест приложения и добавьте `defaultInstallScope` свойство.</span><span class="sxs-lookup"><span data-stu-id="d48f4-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="d48f4-113">Установите значение `personal` , `team` или `groupchat` `meetings` (см. пример ниже).</span><span class="sxs-lookup"><span data-stu-id="d48f4-113">Set a value of `personal`, `team`, `groupchat`, or `meetings` (see an example below).</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="d48f4-114">Дополнительные сведения см. в [схеме манифеста приложения.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="d48f4-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="d48f4-115">Настройка возможностей по умолчанию для общих областей</span><span class="sxs-lookup"><span data-stu-id="d48f4-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="d48f4-116">Настройка возможностей по умолчанию при установке приложения для группы, собрания или чата.</span><span class="sxs-lookup"><span data-stu-id="d48f4-116">Configure the default capability when your app is installed for a team, meeting, or chat.</span></span>

<span data-ttu-id="d48f4-117">**Настройка сведений в манифесте приложения**</span><span class="sxs-lookup"><span data-stu-id="d48f4-117">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="d48f4-118">Откройте манифест приложения и добавьте `defaultGroupCapability` в него свойство.</span><span class="sxs-lookup"><span data-stu-id="d48f4-118">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="d48f4-119">Сохранение обновлений.</span><span class="sxs-lookup"><span data-stu-id="d48f4-119">Save the updates.</span></span>

    <span data-ttu-id="d48f4-120">Ниже приводится пример JSON:</span><span class="sxs-lookup"><span data-stu-id="d48f4-120">Following is a JSON example:</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```
> [!NOTE]
> <span data-ttu-id="d48f4-121">Сведения о полной схеме см. в [схеме манифеста.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="d48f4-121">For information on full schema, see [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="d48f4-122">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="d48f4-122">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d48f4-123">Выбор способа распространения приложения</span><span class="sxs-lookup"><span data-stu-id="d48f4-123">Choose how to distribute your app</span></span>](overview.md)
