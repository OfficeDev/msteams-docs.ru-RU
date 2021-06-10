---
title: DevTools для вкладок Microsoft Teams
description: Описывает, как добраться до DevTools при использовании Microsoft Teams настольного клиента
localization_priority: Normal
ms.topic: how-to
keywords: devtools отладка мобильных средств разработки настольных компьютеров chrome для настольных компьютеров
ms.openlocfilehash: 70c9a2bab94ceb97e8dcd5cf5cdb98261d037f74
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101830"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="17ad0-104">DevTools для вкладок Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="17ad0-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="17ad0-105">Когда Teams в браузере, легко получить доступ к devTools браузера: F12 на Windows или Command-Option-I на MacOS.</span><span class="sxs-lookup"><span data-stu-id="17ad0-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="17ad0-106">DevTools предоставляет вам доступ к:</span><span class="sxs-lookup"><span data-stu-id="17ad0-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="17ad0-107">Просмотр журналов консоли.</span><span class="sxs-lookup"><span data-stu-id="17ad0-107">View console logs.</span></span>
1. <span data-ttu-id="17ad0-108">Просмотр или изменение HTML-запросов, CSS и сетевых запросов во время работы.</span><span class="sxs-lookup"><span data-stu-id="17ad0-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="17ad0-109">Добавьте breakpoints в код JavaScript и выполните интерактивную отладку.</span><span class="sxs-lookup"><span data-stu-id="17ad0-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="17ad0-110">Эта функция доступна только для клиентов на настольных компьютерах и Android **после** Developer Preview включена.</span><span class="sxs-lookup"><span data-stu-id="17ad0-110">The feature is only available for desktop and Android clients after the **Developer Preview** has been enabled.</span></span> <span data-ttu-id="17ad0-111">Дополнительные сведения см. в [обзоре Как включить предварительный просмотр разработчика.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="17ad0-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-on-the-desktop"></a><span data-ttu-id="17ad0-112">Доступ к DevTools на рабочем столе</span><span class="sxs-lookup"><span data-stu-id="17ad0-112">Access DevTools on the desktop</span></span>

<span data-ttu-id="17ad0-113">Несмотря на то, что веб-версия и Teams практически одинаковы, существуют некоторые различия в проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="17ad0-113">While the web version and the desktop version of Teams are almost the same, there are some differences concerning authentication.</span></span> <span data-ttu-id="17ad0-114">Иногда единственный способ выяснить, что происходит, это использовать DevTools.</span><span class="sxs-lookup"><span data-stu-id="17ad0-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="17ad0-115">Чтобы использовать DevTools в настольном клиенте, необходимо:</span><span class="sxs-lookup"><span data-stu-id="17ad0-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="17ad0-116">Убедитесь, что вы [включили предварительный просмотр разработчика.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="17ad0-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="17ad0-117">Откройте вкладку, чтобы вам было что проверить с помощью DevTools.</span><span class="sxs-lookup"><span data-stu-id="17ad0-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="17ad0-118">Откройте DevTools одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="17ad0-118">Open the DevTools one of the following ways:</span></span>
    * <span data-ttu-id="17ad0-119">На Windows вы открываете DevTools через значок Microsoft Teams в настольном лотке:</span><span class="sxs-lookup"><span data-stu-id="17ad0-119">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span><br>
  <span data-ttu-id="17ad0-120">![Щелкните правой кнопкой мыши, чтобы открыть DevTools](~/assets/images/dev-preview/devtools-right-click.png)</span><span class="sxs-lookup"><span data-stu-id="17ad0-120">![Right-click to open DevTools](~/assets/images/dev-preview/devtools-right-click.png)</span></span>
    * <span data-ttu-id="17ad0-121">На MacOS щелкните значок Microsoft Teams в доке.</span><span class="sxs-lookup"><span data-stu-id="17ad0-121">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="17ad0-122">В следующем примере показано, как DevTools открывают и проверяют диалоговое окно конфигурации вкладок:</span><span class="sxs-lookup"><span data-stu-id="17ad0-122">The following example shows DevTools open and inspecting a tab configuration dialog:</span></span>

   ![Tab и DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-device"></a><span data-ttu-id="17ad0-124">Доступ к DevTools с android-устройства</span><span class="sxs-lookup"><span data-stu-id="17ad0-124">Access DevTools from an Android device</span></span>

<span data-ttu-id="17ad0-125">Вы также можете включить DevTools из Teams Android клиента.</span><span class="sxs-lookup"><span data-stu-id="17ad0-125">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="17ad0-126">Чтобы включить DevTools, необходимо:</span><span class="sxs-lookup"><span data-stu-id="17ad0-126">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="17ad0-127">Включить [предварительный просмотр разработчика.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="17ad0-127">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="17ad0-128">Подключение устройство на настольный компьютер и установите устройство Android для удаленной [отладки.](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="17ad0-128">Connect your device to your desktop computer, and set up your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="17ad0-129">В браузере Chrome откройте `chrome://inspect/#devices` .</span><span class="sxs-lookup"><span data-stu-id="17ad0-129">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="17ad0-130">Выберите  инспектировать в вкладке, необходимой для отладки, как на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="17ad0-130">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
