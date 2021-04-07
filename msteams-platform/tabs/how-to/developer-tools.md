---
title: DevTools для вкладок Microsoft Teams
description: Описывает, как добраться до DevTools при использовании настольного клиента Microsoft Teams
ms.topic: how-to
keywords: devtools отладка мобильных средств разработки настольных компьютеров chrome для настольных компьютеров
ms.openlocfilehash: 1bf7d246136a24316309ae144ac9552c5fd4f57d
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596275"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="84606-104">DevTools для вкладок Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="84606-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="84606-105">Когда Teams работает в браузере, легко получить доступ к devTools браузера: F12 (на Windows) или Command-Option-I (на MacOS).</span><span class="sxs-lookup"><span data-stu-id="84606-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="84606-106">DevTools предоставляет вам доступ к:</span><span class="sxs-lookup"><span data-stu-id="84606-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="84606-107">Просмотр журналов консоли.</span><span class="sxs-lookup"><span data-stu-id="84606-107">View console logs.</span></span>
1. <span data-ttu-id="84606-108">Просмотр и изменение html-запросов, css и сетевых запросов во время работы.</span><span class="sxs-lookup"><span data-stu-id="84606-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="84606-109">Добавьте точки брейк-пойнтов в код JavaScript и выполните интерактивную отладку.</span><span class="sxs-lookup"><span data-stu-id="84606-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="84606-110">Функция доступна только в настольных и android-клиентах после Developer Preview включена.</span><span class="sxs-lookup"><span data-stu-id="84606-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="84606-111">Дополнительные [сведения см.](~/resources/dev-preview/developer-preview-intro.md) в Developer Preview.</span><span class="sxs-lookup"><span data-stu-id="84606-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="84606-112">Доступ к DevTools на рабочем столе</span><span class="sxs-lookup"><span data-stu-id="84606-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="84606-113">Несмотря на то, что веб-версия Teams и десктопная версия команд практически одинаковы, существуют некоторые различия, особенно в отношении проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="84606-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="84606-114">Иногда единственный способ выяснить, что происходит, это использовать DevTools.</span><span class="sxs-lookup"><span data-stu-id="84606-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="84606-115">Вот как добраться до них с настольного клиента Teams.</span><span class="sxs-lookup"><span data-stu-id="84606-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="84606-116">Использование DevTools в настольном клиенте:</span><span class="sxs-lookup"><span data-stu-id="84606-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="84606-117">Убедитесь, что вы включили [предварительный просмотр разработчика](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="84606-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="84606-118">Откройте вкладку, чтобы вам было что проверить с помощью DevTools.</span><span class="sxs-lookup"><span data-stu-id="84606-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="84606-119">Откройте DevTools одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="84606-119">Open the DevTools one of the following ways:</span></span>
    * <span data-ttu-id="84606-120">**Windows.** Выберите значок Teams в настольном лотке.</span><span class="sxs-lookup"><span data-stu-id="84606-120">**Windows**: Select the Teams icon in the desktop tray.</span></span>
    * <span data-ttu-id="84606-121">**macOS.** Выберите значок Teams в доке.</span><span class="sxs-lookup"><span data-stu-id="84606-121">**macOS**: Select the Teams icon in the Dock.</span></span>

<span data-ttu-id="84606-122">На следующем скриншоте показано, как DevTools проверяет элемент в диалоговом окантовке конфигурации вкладок:</span><span class="sxs-lookup"><span data-stu-id="84606-122">The following screenshot shows DevTools inspecting an element in a tab configuration dialog:</span></span>

![Tab и DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="84606-124">Доступ к DevTools от клиента Android</span><span class="sxs-lookup"><span data-stu-id="84606-124">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="84606-125">Вы также можете включить DevTools из клиента Teams Android.</span><span class="sxs-lookup"><span data-stu-id="84606-125">You can also enable the DevTools from the Teams Android client.</span></span>

1. <span data-ttu-id="84606-126">Убедитесь, что вы включили [предварительный просмотр разработчика](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="84606-126">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="84606-127">Подключение устройства к настольному компьютеру и настройка устройства Android для [удаленного отладки](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="84606-127">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="84606-128">В браузере Chrome откройте `chrome://inspect/#devices` .</span><span class="sxs-lookup"><span data-stu-id="84606-128">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="84606-129">Нажмите **кнопку** проверки ниже вкладки, которая необходимо отлажать, как на скриншоте ниже.</span><span class="sxs-lookup"><span data-stu-id="84606-129">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![Android DevTools](~/assets/images/android-devtools.png)
