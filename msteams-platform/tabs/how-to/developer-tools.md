---
title: DevTools для вкладок Microsoft Teams
description: Описание того, как добраться до DevTools при использовании клиента Microsoft Teams для настольных ПК
ms.topic: how-to
keywords: devtools debug mobile chrome desktop client developer tools
ms.openlocfilehash: 8f23a5d56faa00d40451d2bbeadde32f6a5d0f7f
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014581"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="c5b84-104">DevTools для вкладок Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c5b84-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="c5b84-105">Когда Teams работает в браузере, легко получить доступ к devTools браузера: F12 (в Windows) или Command-Option-I (в MacOS).</span><span class="sxs-lookup"><span data-stu-id="c5b84-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="c5b84-106">DevTools предоставляет доступ к:</span><span class="sxs-lookup"><span data-stu-id="c5b84-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="c5b84-107">Просмотр журналов консоли.</span><span class="sxs-lookup"><span data-stu-id="c5b84-107">View console logs.</span></span>
1. <span data-ttu-id="c5b84-108">Просмотр и изменение html-запросов, CSS и сетевых запросов во время работы.</span><span class="sxs-lookup"><span data-stu-id="c5b84-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="c5b84-109">Добавьте точки останова в код JavaScript и выполните интерактивную отладку.</span><span class="sxs-lookup"><span data-stu-id="c5b84-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="c5b84-110">Эта функция доступна только в классических клиентах и клиентах Android Developer Preview включена.</span><span class="sxs-lookup"><span data-stu-id="c5b84-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="c5b84-111">Дополнительные [сведения см. в](~/resources/dev-preview/developer-preview-intro.md) Developer Preview.</span><span class="sxs-lookup"><span data-stu-id="c5b84-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="c5b84-112">Доступ к DevTools на рабочем столе</span><span class="sxs-lookup"><span data-stu-id="c5b84-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="c5b84-113">Несмотря на то что веб-версия Teams и классические версии команд практически не отличаются, существуют некоторые различия, особенно в отношении проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c5b84-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="c5b84-114">Иногда единственным способом выяснить, что происходит, является использование DevTools.</span><span class="sxs-lookup"><span data-stu-id="c5b84-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="c5b84-115">Вот как получить к ним возможность из настольного клиента Teams.</span><span class="sxs-lookup"><span data-stu-id="c5b84-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="c5b84-116">Чтобы использовать DevTools в настольном клиенте:</span><span class="sxs-lookup"><span data-stu-id="c5b84-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="c5b84-117">Убедитесь, что вы включили [предварительную версию для разработчиков](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c5b84-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="c5b84-118">Откройте вкладку, чтобы получить что-то для проверки с помощью DevTools.</span><span class="sxs-lookup"><span data-stu-id="c5b84-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="c5b84-119">Откройте DevTools</span><span class="sxs-lookup"><span data-stu-id="c5b84-119">Open the DevTools</span></span>
    * <span data-ttu-id="c5b84-120">В Windows вы открываете DevTools с помощью значка Microsoft Teams в области рабочего стола:</span><span class="sxs-lookup"><span data-stu-id="c5b84-120">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span>

  ![Щелкните правой кнопкой мыши, чтобы открыть DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * <span data-ttu-id="c5b84-122">В MacOS щелкните значок Microsoft Teams на док-станции.</span><span class="sxs-lookup"><span data-stu-id="c5b84-122">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="c5b84-123">Вот как выглядит вкладка с открытым devTools и выбранным элементом:</span><span class="sxs-lookup"><span data-stu-id="c5b84-123">Here’s what a sample tab looks like with the DevTools open and an element selected:</span></span>

![Tab и DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="c5b84-125">Доступ к DevTools из клиента Android</span><span class="sxs-lookup"><span data-stu-id="c5b84-125">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="c5b84-126">Вы также можете включить DevTools из клиента Teams Android.</span><span class="sxs-lookup"><span data-stu-id="c5b84-126">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="c5b84-127">Для этого:</span><span class="sxs-lookup"><span data-stu-id="c5b84-127">To do so:</span></span>

1. <span data-ttu-id="c5b84-128">Убедитесь, что вы включили [предварительную версию для разработчиков](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c5b84-128">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="c5b84-129">Подключение устройства к настольному компьютеру и настройка устройства с Android для [удаленной отладки](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="c5b84-129">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="c5b84-130">В браузере Chrome откройте `chrome://inspect/#devices` .</span><span class="sxs-lookup"><span data-stu-id="c5b84-130">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="c5b84-131">Щелкните **"Проверить"** под вкладками, которые нужно отлажать, как по снимку экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="c5b84-131">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![Android DevTools](~/assets/images/android-devtools.png)
