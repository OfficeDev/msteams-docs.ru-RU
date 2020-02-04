---
title: Девтулс для вкладок Microsoft Teams
description: В этой статье описывается, как получить доступ к Девтулс при использовании настольного клиента Microsoft Teams
keywords: средства разработчика клиентского рабочего стола Mobile Chrome девтулс Отладка
ms.openlocfilehash: 6c8ac15caf64c979b23155be847e8791988486e6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675416"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="ced0a-104">Девтулс для вкладок Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ced0a-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="ced0a-105">Когда Teams работает в браузере, можно легко получить доступ к Девтулс браузера: F12 (в Windows) или Command-Option-I (на MacOS).</span><span class="sxs-lookup"><span data-stu-id="ced0a-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="ced0a-106">Девтулс предоставляет доступ к следующим:</span><span class="sxs-lookup"><span data-stu-id="ced0a-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="ced0a-107">Просмотр журналов консоли.</span><span class="sxs-lookup"><span data-stu-id="ced0a-107">View console logs.</span></span>
1. <span data-ttu-id="ced0a-108">Просмотр/изменение HTML-, CSS-и сетевых запросов во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="ced0a-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="ced0a-109">Добавьте точки останова в код JavaScript и выполните интерактивную отладку.</span><span class="sxs-lookup"><span data-stu-id="ced0a-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="ced0a-110">Эта функция доступна только в клиентах для настольных ПК и Android после включения предварительной версии для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="ced0a-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="ced0a-111">Узнайте, [как включить предварительный просмотр для разработчиков](~/resources/dev-preview/developer-preview-intro.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="ced0a-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="ced0a-112">Доступ к Девтулс на рабочем столе</span><span class="sxs-lookup"><span data-stu-id="ced0a-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="ced0a-113">Несмотря на то, что веб-версия Teams и версия Teams для настольных систем почти идентичны, существуют некоторые отличия, особенно по отношению к проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="ced0a-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="ced0a-114">Иногда единственный способ понять, что происходит, — использовать Девтулс.</span><span class="sxs-lookup"><span data-stu-id="ced0a-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="ced0a-115">Вот как можно перейти к ним из клиента для настольных ПК Teams.</span><span class="sxs-lookup"><span data-stu-id="ced0a-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="ced0a-116">Чтобы использовать Девтулс в клиенте для настольных ПК:</span><span class="sxs-lookup"><span data-stu-id="ced0a-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="ced0a-117">Убедитесь, что вы включили [Предварительный просмотр для разработчиков](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ced0a-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="ced0a-118">Откройте вкладку, чтобы ознакомиться с Девтулс.</span><span class="sxs-lookup"><span data-stu-id="ced0a-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="ced0a-119">Открытие Девтулс</span><span class="sxs-lookup"><span data-stu-id="ced0a-119">Open the DevTools</span></span>
    * <span data-ttu-id="ced0a-120">В Windows вы открываете Девтулс через значок Microsoft Teams в панели рабочего стола:</span><span class="sxs-lookup"><span data-stu-id="ced0a-120">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span>

  ![Щелкните правой кнопкой мыши, чтобы открыть Девтулс](~/assets/images/dev-preview/devtools-right-click.png)

    * <span data-ttu-id="ced0a-122">В MacOS щелкните значок Microsoft Teams (Microsoft Teams) на док.</span><span class="sxs-lookup"><span data-stu-id="ced0a-122">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="ced0a-123">Ниже показано, как выглядит пример вкладки с открытым Девтулс и выбранным элементом:</span><span class="sxs-lookup"><span data-stu-id="ced0a-123">Here’s what a sample tab looks like with the DevTools open and an element selected:</span></span>

![Tab и Девтулс](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="ced0a-125">Доступ к Девтулс из клиента Android</span><span class="sxs-lookup"><span data-stu-id="ced0a-125">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="ced0a-126">Вы также можете включить Девтулс из клиента Teams Android.</span><span class="sxs-lookup"><span data-stu-id="ced0a-126">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="ced0a-127">Для этого:</span><span class="sxs-lookup"><span data-stu-id="ced0a-127">To do so:</span></span>

1. <span data-ttu-id="ced0a-128">Убедитесь, что вы включили [Предварительный просмотр для разработчиков](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ced0a-128">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="ced0a-129">Подключение устройства к настольному компьютеру и Настройка устройства с Android для [удаленной отладки](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="ced0a-129">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="ced0a-130">В браузере Chrome откройте `chrome://inspect/#devices`меню.</span><span class="sxs-lookup"><span data-stu-id="ced0a-130">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="ced0a-131">Нажмите кнопку **проверить** ниже вкладки, которую вы хотите отладить, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="ced0a-131">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![Девтулс Android](~/assets/images/android-devtools.png)
