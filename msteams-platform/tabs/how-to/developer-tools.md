---
title: DevTools для вкладок Microsoft Teams
description: Описывает, как добраться до DevTools при использовании настольного клиента Microsoft Teams
ms.topic: how-to
keywords: devtools отладка мобильных средств разработки настольных компьютеров chrome для настольных компьютеров
ms.openlocfilehash: 1c540c94adc080d9495097f8e3b427eeb14c56d8
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634743"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="1cb57-104">DevTools для вкладок Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1cb57-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="1cb57-105">Когда Teams работает в браузере, легко получить доступ к devTools браузера: F12 на Windows или Command-Option-I на MacOS.</span><span class="sxs-lookup"><span data-stu-id="1cb57-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="1cb57-106">DevTools предоставляет вам доступ к:</span><span class="sxs-lookup"><span data-stu-id="1cb57-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="1cb57-107">Просмотр журналов консоли.</span><span class="sxs-lookup"><span data-stu-id="1cb57-107">View console logs.</span></span>
1. <span data-ttu-id="1cb57-108">Просмотр или изменение HTML-запросов, CSS и сетевых запросов во время работы.</span><span class="sxs-lookup"><span data-stu-id="1cb57-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="1cb57-109">Добавьте breakpoints в код JavaScript и выполните интерактивную отладку.</span><span class="sxs-lookup"><span data-stu-id="1cb57-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="1cb57-110">Функция доступна только в настольных компьютерах и android-клиентах **после Developer Preview** включена.</span><span class="sxs-lookup"><span data-stu-id="1cb57-110">The feature is only available in desktop and Android clients after **Developer Preview** has been enabled.</span></span> <span data-ttu-id="1cb57-111">Дополнительные сведения см. в [обзоре Как включить предварительный просмотр разработчика.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="1cb57-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-in-the-desktop"></a><span data-ttu-id="1cb57-112">Доступ к DevTools на рабочем столе</span><span class="sxs-lookup"><span data-stu-id="1cb57-112">Access DevTools in the Desktop</span></span>

<span data-ttu-id="1cb57-113">Несмотря на то, что веб-версия и десктопная версия Teams практически одинаковы, существуют некоторые различия в отношении проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="1cb57-113">While the web version and the desktop version of Teams are almost exactly the same, there are some differences with respect to authentication.</span></span> <span data-ttu-id="1cb57-114">Иногда единственный способ выяснить, что происходит, это использовать DevTools.</span><span class="sxs-lookup"><span data-stu-id="1cb57-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="1cb57-115">Чтобы использовать DevTools в настольном клиенте, необходимо:</span><span class="sxs-lookup"><span data-stu-id="1cb57-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="1cb57-116">Убедитесь, что вы [включили предварительный просмотр разработчика.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="1cb57-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="1cb57-117">Откройте вкладку, чтобы вам было что проверить с помощью DevTools.</span><span class="sxs-lookup"><span data-stu-id="1cb57-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="1cb57-118">Откройте DevTools одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="1cb57-118">Open the DevTools in one of the following ways:</span></span>
    * <span data-ttu-id="1cb57-119">**Windows.** Выберите значок Teams в настольном лотке.</span><span class="sxs-lookup"><span data-stu-id="1cb57-119">**Windows**: Select the Teams icon in the desktop tray.</span></span>
    * <span data-ttu-id="1cb57-120">**MacOS.** Выберите значок Teams в доке.</span><span class="sxs-lookup"><span data-stu-id="1cb57-120">**MacOS**: Select the Teams icon in the Dock.</span></span>
 
   <span data-ttu-id="1cb57-121">На следующем изображении показано, как DevTools проверяет элемент в диалоговом окантовке конфигурации вкладок:</span><span class="sxs-lookup"><span data-stu-id="1cb57-121">The following image shows DevTools inspecting an element in a tab configuration dialog:</span></span>

   ![Tab и DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a><span data-ttu-id="1cb57-123">Доступ к DevTools от клиента Android</span><span class="sxs-lookup"><span data-stu-id="1cb57-123">Access DevTools from an Android client</span></span>

<span data-ttu-id="1cb57-124">Вы также можете включить DevTools из клиента Teams Android.</span><span class="sxs-lookup"><span data-stu-id="1cb57-124">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="1cb57-125">Чтобы включить DevTools, необходимо:</span><span class="sxs-lookup"><span data-stu-id="1cb57-125">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="1cb57-126">Включить [предварительный просмотр разработчика.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="1cb57-126">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="1cb57-127">Подключение устройства к настольному компьютеру и настройка устройства Android для [удаленного отладки.](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="1cb57-127">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="1cb57-128">В браузере Chrome откройте `chrome://inspect/#devices` .</span><span class="sxs-lookup"><span data-stu-id="1cb57-128">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="1cb57-129">Выберите  инспектировать в вкладке, необходимой для отладки, как на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="1cb57-129">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
