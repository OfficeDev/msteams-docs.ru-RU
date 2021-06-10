---
title: Требования к вкладке
author: laujan
description: Каждая вкладка в Microsoft Teams должна соответствовать этим требованиям.
keywords: команды вкладки группового канала настраиваются
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 50d529697a80ca9ba78921009405f18fa021e802
ms.sourcegitcommit: 45c66faef8145abb903ef7118b9fa914c12aba2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/03/2021
ms.locfileid: "52736763"
---
# <a name="tab-requirements"></a><span data-ttu-id="71160-104">Требования к вкладке</span><span class="sxs-lookup"><span data-stu-id="71160-104">Tab requirements</span></span>

<span data-ttu-id="71160-105">Teams вкладки должны соответствовать следующим требованиям:</span><span class="sxs-lookup"><span data-stu-id="71160-105">Teams tabs must adhere to the following requirements:</span></span>

* <span data-ttu-id="71160-106">Необходимо разрешить, чтобы страницы вкладок обслуживались в iFrame с помощью заглавных заглавных ответов http-службы X-Frame-Options и Content-Security-Policy HTTP.</span><span class="sxs-lookup"><span data-stu-id="71160-106">You must allow your tab pages to be served in an iFrame, using X-Frame-Options and Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="71160-107">Установите заглавную: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="71160-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="71160-108">Для совместимости Internet Explorer 11 установите `X-Content-Security-Policy` .</span><span class="sxs-lookup"><span data-stu-id="71160-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy`.</span></span>
  * <span data-ttu-id="71160-109">Поочередно установите заглавную `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="71160-109">Alternately, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="71160-110">Этот заголовок является обесценим, но по-прежнему принимается большинством браузеров.</span><span class="sxs-lookup"><span data-stu-id="71160-110">This header is deprecated but still accepted by most browsers.</span></span>
* <span data-ttu-id="71160-111">Как правило, в качестве защиты от нажатия кнопки страницы входа не отрисовка в iFrames.</span><span class="sxs-lookup"><span data-stu-id="71160-111">Typically, as a safeguard against click-jacking, login pages do not render in iFrames.</span></span> <span data-ttu-id="71160-112">Логике проверки подлинности необходимо использовать метод, не перенаправление.</span><span class="sxs-lookup"><span data-stu-id="71160-112">Your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="71160-113">Например, используйте проверку подлинности на основе маркеров или файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="71160-113">For example, use token-based or cookie-based authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71160-114">Chrome 80, запланированный на выпуск в начале 2020 г., вводит новые значения cookie и по умолчанию вводит политики cookie.</span><span class="sxs-lookup"><span data-stu-id="71160-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="71160-115">Рекомендуется установить предназначенное использование для файлов cookie, а не полагаться на поведение браузера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="71160-115">It is recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="71160-116">Дополнительные сведения см. в обновлении [атрибута cookie SameSite 2020.](../../resources/samesite-cookie-update.md)</span><span class="sxs-lookup"><span data-stu-id="71160-116">For more information, see [SameSite cookie attribute 2020 update](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="71160-117">Браузеры придерживаются ограничения политики одного происхождения, которое не позволяет веб-странице делать запросы в другой домен, чем тот, который обслуживал веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="71160-117">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="71160-118">Однако вы можете перенаправить конфигурацию или страницу контента на другой домен или поддомен.</span><span class="sxs-lookup"><span data-stu-id="71160-118">However, you can redirect the configuration or content page to another domain or subdomain.</span></span> <span data-ttu-id="71160-119">Логика навигации между доменами должна позволить клиенту Teams проверить происхождение со статическим списком validDomains в манифесте приложения при загрузке или общении со вкладкой.</span><span class="sxs-lookup"><span data-stu-id="71160-119">Your cross-domain navigation logic must allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="71160-120">Чтобы создать бесшовное впечатление, необходимо создать стиль вкладок на основе Teams темы, дизайна и намерения клиента.</span><span class="sxs-lookup"><span data-stu-id="71160-120">To create a seamless experience, you must style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="71160-121">Обычно вкладки лучше всего работают, когда они построены для решения определенных потребностей и фокуса на небольшом наборе задач или подмножество данных, соответствующих расположению канала вкладки.</span><span class="sxs-lookup"><span data-stu-id="71160-121">Typically, tabs work best when they are built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="71160-122">На странице контента добавьте ссылку на [SDK](/javascript/api/overview/msteams-client) клиента JavaScript Microsoft Teams с помощью тегов скриптов.</span><span class="sxs-lookup"><span data-stu-id="71160-122">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="71160-123">После загрузки страницы сделайте вызов, в противном случае страница `microsoftTeams.initialize()` не отображается.</span><span class="sxs-lookup"><span data-stu-id="71160-123">After your page loads, make a call to `microsoftTeams.initialize()`, otherwise your page is not displayed.</span></span>

* <span data-ttu-id="71160-124">Для проверки подлинности для мобильных клиентов необходимо обновить Teams JavaScript SDK по крайней мере до версии 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="71160-124">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="71160-125">Если вы хотите, чтобы вкладка канала или группы Teams мобильных клиентов, конфигурация должна иметь значение `setSettings()` `websiteUrl` свойства.</span><span class="sxs-lookup"><span data-stu-id="71160-125">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

* <span data-ttu-id="71160-126">Вкладка MS Teams не поддерживает возможность загрузки веб-сайтов интрасети, которые используют самозаверяемые сертификаты.</span><span class="sxs-lookup"><span data-stu-id="71160-126">MS Teams tab does not support the ability to load intranet websites that use self-signed certificates.</span></span>

## <a name="next-step"></a><span data-ttu-id="71160-127">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="71160-127">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="71160-128">Создайте настраиваемую личную вкладку с Node.js и генератором Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="71160-128">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)
