---
title: Необходимые условия
author: surbhigupta
description: Каждая вкладка в Microsoft Teams должна соответствовать этим требованиям.
keywords: команды вкладки группового канала настраиваются
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b54fc7235132a9253f6eecc62417f786bf4aa45c
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140189"
---
# <a name="prerequisites"></a><span data-ttu-id="249b2-104">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="249b2-104">Prerequisites</span></span>

<span data-ttu-id="249b2-105">Teams должны придерживаться следующих обязательных условий:</span><span class="sxs-lookup"><span data-stu-id="249b2-105">Teams tabs must adhere to the following prerequisites:</span></span>

* <span data-ttu-id="249b2-106">Необходимо разрешить показывать страницы вкладок в iFrame с помощью заглавных заглавных ответов X-Frame-Options и Content-Security-Policy HTTP.</span><span class="sxs-lookup"><span data-stu-id="249b2-106">You must allow your tab pages to be shown in an iFrame, using X-Frame-Options and Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="249b2-107">Установите заглавную: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="249b2-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="249b2-108">Для совместимости Internet Explorer 11 установите `X-Content-Security-Policy` .</span><span class="sxs-lookup"><span data-stu-id="249b2-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy`.</span></span>
  * <span data-ttu-id="249b2-109">Поочередно установите заглавную `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="249b2-109">Alternately, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="249b2-110">Этот заголовок является обесценим, но по-прежнему принимается большинством браузеров.</span><span class="sxs-lookup"><span data-stu-id="249b2-110">This header is deprecated but still accepted by most browsers.</span></span>

* <span data-ttu-id="249b2-111">Как правило, в качестве защиты от угона кликов страницы входа в iFrames не отрисовкуются.</span><span class="sxs-lookup"><span data-stu-id="249b2-111">Typically, as a safeguard against clickjacking, login pages do not render in iFrames.</span></span> <span data-ttu-id="249b2-112">Логике проверки подлинности необходимо использовать метод, не перенаправление.</span><span class="sxs-lookup"><span data-stu-id="249b2-112">Your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="249b2-113">Например, используйте проверку подлинности на основе маркеров или файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="249b2-113">For example, use token-based or cookie-based authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="249b2-114">Chrome 80, запланированный на выпуск в начале 2020 г., вводит новые значения cookie и по умолчанию вводит политики cookie.</span><span class="sxs-lookup"><span data-stu-id="249b2-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="249b2-115">Рекомендуется установить предназначенное использование для файлов cookie, а не полагаться на поведение браузера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="249b2-115">It is recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="249b2-116">Дополнительные сведения см. в [атрибуте Cookie SameSite.](../../resources/samesite-cookie-update.md)</span><span class="sxs-lookup"><span data-stu-id="249b2-116">For more information, see [SameSite cookie attribute](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="249b2-117">Браузеры придерживаются ограничения политики одного происхождения.</span><span class="sxs-lookup"><span data-stu-id="249b2-117">Browsers adhere to a same-origin policy restriction.</span></span> <span data-ttu-id="249b2-118">Это не позволяет веб-страницам делать запросы на различные домены, чем обслуживаемая веб-страница.</span><span class="sxs-lookup"><span data-stu-id="249b2-118">It prevents webpages from making requests to different domains than the served web page.</span></span> <span data-ttu-id="249b2-119">Однако вы можете перенаправить конфигурацию или страницу контента на другой домен или поддомен.</span><span class="sxs-lookup"><span data-stu-id="249b2-119">However, you can redirect the configuration or content page to another domain or subdomain.</span></span> <span data-ttu-id="249b2-120">Логика навигации между доменами должна позволить клиенту Teams проверить происхождение со статическим списком в манифесте приложения при загрузке или общении с `validDomains` вкладкой.</span><span class="sxs-lookup"><span data-stu-id="249b2-120">Your cross-domain navigation logic must allow the Teams client to validate the origin against a static `validDomains` list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="249b2-121">Вкладки необходимо стильировать в зависимости Teams темы, дизайна и намерения клиента.</span><span class="sxs-lookup"><span data-stu-id="249b2-121">You must style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="249b2-122">Обычно вкладки лучше всего работают, когда они построены для решения определенных потребностей и фокуса на небольшом наборе задач или подмножество данных, соответствующих расположению канала вкладки.</span><span class="sxs-lookup"><span data-stu-id="249b2-122">Typically, tabs work best when they are built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="249b2-123">На странице контента добавьте ссылку на [SDK](/javascript/api/overview/msteams-client) клиента JavaScript Microsoft Teams с помощью тегов скриптов.</span><span class="sxs-lookup"><span data-stu-id="249b2-123">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="249b2-124">После загрузки страницы сделайте вызов, в противном случае страница `microsoftTeams.initialize()` не отображается.</span><span class="sxs-lookup"><span data-stu-id="249b2-124">After your page loads, make a call to `microsoftTeams.initialize()`, otherwise your page is not displayed.</span></span>

* <span data-ttu-id="249b2-125">Для проверки подлинности для мобильных клиентов необходимо обновить Teams JavaScript SDK по крайней мере до версии 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="249b2-125">For authentication to work on mobile clients, you must upgrade Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="249b2-126">Если вы хотите, чтобы вкладка канала или группы Teams мобильных клиентов, конфигурация должна иметь значение `setSettings()` `websiteUrl` свойства.</span><span class="sxs-lookup"><span data-stu-id="249b2-126">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

* <span data-ttu-id="249b2-127">Вкладка MS Teams не поддерживает возможность загрузки веб-сайтов интрасети, которые используют самозаверяемые сертификаты.</span><span class="sxs-lookup"><span data-stu-id="249b2-127">MS Teams tab does not support the ability to load intranet websites that use self-signed certificates.</span></span>

## <a name="see-also"></a><span data-ttu-id="249b2-128">См. также</span><span class="sxs-lookup"><span data-stu-id="249b2-128">See also</span></span>

* [<span data-ttu-id="249b2-129">Teams вкладки</span><span class="sxs-lookup"><span data-stu-id="249b2-129">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="249b2-130">Создание вкладки канала или группы</span><span class="sxs-lookup"><span data-stu-id="249b2-130">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="249b2-131">Создать страницу контента</span><span class="sxs-lookup"><span data-stu-id="249b2-131">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="249b2-132">Создать страницу конфигурации</span><span class="sxs-lookup"><span data-stu-id="249b2-132">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="249b2-133">Создание страницы удаления для вкладки</span><span class="sxs-lookup"><span data-stu-id="249b2-133">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="249b2-134">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="249b2-134">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="249b2-135">Получение контекста для вкладки</span><span class="sxs-lookup"><span data-stu-id="249b2-135">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="249b2-136">Создание вкладок с использованием адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="249b2-136">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="249b2-137">Предварительный просмотр для ссылки "Вкладки" и представление стадий</span><span class="sxs-lookup"><span data-stu-id="249b2-137">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
* [<span data-ttu-id="249b2-138">Создание вкладок бесед</span><span class="sxs-lookup"><span data-stu-id="249b2-138">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)
* [<span data-ttu-id="249b2-139">Изменения полей вкладок</span><span class="sxs-lookup"><span data-stu-id="249b2-139">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)

## <a name="next-step"></a><span data-ttu-id="249b2-140">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="249b2-140">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="249b2-141">Создать личную вкладку</span><span class="sxs-lookup"><span data-stu-id="249b2-141">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
