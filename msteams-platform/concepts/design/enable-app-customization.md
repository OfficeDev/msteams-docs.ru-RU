---
title: Включить настройку приложения
author: heath-hamilton
description: Поймите, Teams администраторы могут настроить ваше приложение для своей организации.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: bf1b43629c87dd4123520c634772e5dea14e0bb5
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915085"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a><span data-ttu-id="595c0-103">Включить настройку Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="595c0-103">Enable your Microsoft Teams app to be customized</span></span>

<span data-ttu-id="595c0-104">Вы можете разрешить клиентам настраивать некоторые аспекты вашего Microsoft Teams в центре администрирования Teams.</span><span class="sxs-lookup"><span data-stu-id="595c0-104">You can allow customers to customize some aspects of your Microsoft Teams app in the Teams admin center.</span></span> <span data-ttu-id="595c0-105">Эта функция поддерживается только для приложений, опубликованных в Teams магазине.</span><span class="sxs-lookup"><span data-stu-id="595c0-105">This feature is supported only for apps published to the Teams store.</span></span> <span data-ttu-id="595c0-106">Дополнительные приложения и приложения, опубликованные для организации, не могут быть настроены.</span><span class="sxs-lookup"><span data-stu-id="595c0-106">Sideloaded apps and apps published for an org can't be customized.</span></span>

<span data-ttu-id="595c0-107">Некоторые возможные примеры этой функции включают в себя:</span><span class="sxs-lookup"><span data-stu-id="595c0-107">Some possible examples of this feature include:</span></span>

* <span data-ttu-id="595c0-108">Изменение цвета акцента приложения в соответствие с брендом организации.</span><span class="sxs-lookup"><span data-stu-id="595c0-108">Changing the app's accent color to match an org's brand.</span></span>
* <span data-ttu-id="595c0-109">Обновление имени приложения от *Contoso* до *Агента Contoso*, которое пользователи в организации увидят.</span><span class="sxs-lookup"><span data-stu-id="595c0-109">Updating the app name from *Contoso* to *Contoso Agent*, which is the name users in the org will see.</span></span> <span data-ttu-id="595c0-110">(Примечание. Пользователи, добавляя соединители в чат или канал, по-прежнему будут видеть исходное имя *приложения Contoso*.)</span><span class="sxs-lookup"><span data-stu-id="595c0-110">(Note: Users adding a connector to a chat or a channel will still see the original app name, *Contoso*.)</span></span>

<span data-ttu-id="595c0-111">Эту функцию можно включить на [портале разработчиков для Teams.](https://dev.teams.microsoft.com/home)</span><span class="sxs-lookup"><span data-stu-id="595c0-111">You can enable this feature in the [Developer Portal for Teams](https://dev.teams.microsoft.com/home).</span></span> <span data-ttu-id="595c0-112">Это настраивает, которые недоступны в версиях до `configurableProperties` 1.10 манифеста Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="595c0-112">This configures `configurableProperties`, which aren't available in versions prior to 1.10 of the Teams app manifest.</span></span>

## <a name="test-your-app"></a><span data-ttu-id="595c0-113">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="595c0-113">Test your app</span></span>

<span data-ttu-id="595c0-114">Вы не можете проверить эту функцию во время разработки.</span><span class="sxs-lookup"><span data-stu-id="595c0-114">You cannot test this feature during development.</span></span> <span data-ttu-id="595c0-115">Настройка приложения не поддерживается для загрузки или публикации в каталоге приложений организации.</span><span class="sxs-lookup"><span data-stu-id="595c0-115">App customization is not supported for sideloading or publishing to an organization's app catalog.</span></span>

## <a name="user-considerations"></a><span data-ttu-id="595c0-116">Соображения пользователя</span><span class="sxs-lookup"><span data-stu-id="595c0-116">User considerations</span></span>

<span data-ttu-id="595c0-117">В качестве издателя приложения предоокать следующие сведения клиентам в Teams администраторов:</span><span class="sxs-lookup"><span data-stu-id="595c0-117">As the app publisher, provide the following information to customers in Teams admins:</span></span>
* <span data-ttu-id="595c0-118">Включай примечание, в которой рекомендуется протестировать изменения настройки в Teams тестовом клиенте перед внесением изменений в производственную среду.</span><span class="sxs-lookup"><span data-stu-id="595c0-118">Include a note recommending to test customization changes in a Teams test tenant before making changes in their production environment.</span></span> 
* <span data-ttu-id="595c0-119">Предокарабка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="595c0-119">Provide best practices for how to customize your app.</span></span>

## <a name="see-also"></a><span data-ttu-id="595c0-120">См. также</span><span class="sxs-lookup"><span data-stu-id="595c0-120">See also</span></span>

* [<span data-ttu-id="595c0-121">Настройка приложений в центре Teams администрирования</span><span class="sxs-lookup"><span data-stu-id="595c0-121">Customize apps in the Teams admin center</span></span>](/MicrosoftTeams/customize-apps)
