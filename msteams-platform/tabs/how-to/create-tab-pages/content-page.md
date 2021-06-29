---
title: Создать страницу контента
author: surbhigupta
description: создание страницы контента
keywords: группы вкладок группового канала, настраиваемые статическими
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1276fdac2d3a30836b574b8e51b99fcbd7a415d2
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179736"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="ab67f-104">Создание страницы контента для вкладки</span><span class="sxs-lookup"><span data-stu-id="ab67f-104">Create a content page for your tab</span></span>

<span data-ttu-id="ab67f-105">Страница контента — это веб-страница, отрисовка в Teams клиенте.</span><span class="sxs-lookup"><span data-stu-id="ab67f-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="ab67f-106">Они являются частью:</span><span class="sxs-lookup"><span data-stu-id="ab67f-106">These are part of:</span></span>

* <span data-ttu-id="ab67f-107">Настраиваемая вкладка с личным охватом. В этом случае страница контента является первой страницей, с которой сталкивается пользователь.</span><span class="sxs-lookup"><span data-stu-id="ab67f-107">A personal-scoped custom tab: In this case, the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="ab67f-108">Настраиваемая вкладка канала или группы. Страница контента отображается после пин-кодов пользователя и настраивает вкладку в соответствующем контексте.</span><span class="sxs-lookup"><span data-stu-id="ab67f-108">A channel or group custom tab: The content page is displayed after the user pins and configures the tab in the appropriate context.</span></span>
* <span data-ttu-id="ab67f-109">Модуль [задач.](~/task-modules-and-cards/what-are-task-modules.md)Вы можете создать страницу контента и встраить ее в веб-просмотр внутри модуля задач.</span><span class="sxs-lookup"><span data-stu-id="ab67f-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md): You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="ab67f-110">Страница отрисовка в модальной всплываемой области.</span><span class="sxs-lookup"><span data-stu-id="ab67f-110">The page is rendered inside the modal pop-up.</span></span>

<span data-ttu-id="ab67f-111">Эта статья посвящена использованию страниц контента в качестве вкладок; однако большинство указаний здесь применяется независимо от того, как страница контента представлена пользователю.</span><span class="sxs-lookup"><span data-stu-id="ab67f-111">This article is specific to using content pages as tabs; however the majority of the guidance here applies regardless of how the content page is presented to the user.</span></span>

## <a name="tab-content-and-design-guidelines"></a><span data-ttu-id="ab67f-112">Рекомендации по контенту и дизайну вкладок</span><span class="sxs-lookup"><span data-stu-id="ab67f-112">Tab content and design guidelines</span></span>

<span data-ttu-id="ab67f-113">Общая цель вкладки — предоставить доступ к содержательному и привлекательному контенту, который имеет практическое значение и очевидная цель.</span><span class="sxs-lookup"><span data-stu-id="ab67f-113">Your tab's overall objective is to provide access to meaningful and engaging content that has practical value and an evident purpose.</span></span> <span data-ttu-id="ab67f-114">Необходимо сосредоточиться на том, чтобы сделать дизайн вкладки чистым, интуитивно понятным и захватывающим контентом.</span><span class="sxs-lookup"><span data-stu-id="ab67f-114">You must focus on making your tab design clean, navigation intuitive, and content immersive.</span></span>

<span data-ttu-id="ab67f-115">Дополнительные сведения см. [в рекомендациях](~/tabs/design/tabs.md) по разработке [вкладок и Microsoft Teams проверки хранения.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)</span><span class="sxs-lookup"><span data-stu-id="ab67f-115">For more information, see [tab design guidelines](~/tabs/design/tabs.md) and [Microsoft Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="ab67f-116">Интеграция кода с Teams</span><span class="sxs-lookup"><span data-stu-id="ab67f-116">Integrate your code with Teams</span></span>

<span data-ttu-id="ab67f-117">Чтобы ваша страница отображалась в Teams, необходимо включить Microsoft Teams [клиента JavaScript sDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и включить вызов после загрузки `microsoftTeams.initialize()` страницы.</span><span class="sxs-lookup"><span data-stu-id="ab67f-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> 

<span data-ttu-id="ab67f-118">В следующем коде приводится пример взаимодействия страницы и Teams клиента:</span><span class="sxs-lookup"><span data-stu-id="ab67f-118">The following code provides an example of how your page and the Teams client communicate:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    microsoftTeams.initialize();
    </script>
...
</body>
```

## <a name="access-additional-content"></a><span data-ttu-id="ab67f-119">Доступ к дополнительному контенту</span><span class="sxs-lookup"><span data-stu-id="ab67f-119">Access additional content</span></span>

<span data-ttu-id="ab67f-120">Вы можете получить доступ к дополнительному контенту с помощью SDK для взаимодействия с Teams, создания глубоких ссылок, использования модулей задач и проверки того, включены ли URL-домены в `validDomains` массив.</span><span class="sxs-lookup"><span data-stu-id="ab67f-120">You can access additional content by using the SDK to interact with Teams, creating deep links, using task modules, and verifying if URL domains are included in the `validDomains` array.</span></span>

### <a name="use-the-sdk-to-interact-with-teams"></a><span data-ttu-id="ab67f-121">Используйте SDK для взаимодействия с Teams</span><span class="sxs-lookup"><span data-stu-id="ab67f-121">Use the SDK to interact with Teams</span></span>

<span data-ttu-id="ab67f-122">Клиентская [Teams JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) предоставляет множество дополнительных функций, которые можно найти полезными при разработке страницы контента.</span><span class="sxs-lookup"><span data-stu-id="ab67f-122">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions that you can find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="ab67f-123">Прямые ссылки</span><span class="sxs-lookup"><span data-stu-id="ab67f-123">Deep links</span></span>

<span data-ttu-id="ab67f-124">Можно создавать глубокие ссылки на сущности в Teams.</span><span class="sxs-lookup"><span data-stu-id="ab67f-124">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="ab67f-125">Они используются для создания ссылок, которые переходят к содержимому и сведениям в вкладке. Дополнительные сведения см. в дополнительных сведениях о создании глубоких ссылок на контент и [функции в Teams.](~/concepts/build-and-test/deep-links.md)</span><span class="sxs-lookup"><span data-stu-id="ab67f-125">These are used to create links that navigate to content and information within your tab. For more information, see [create deep links to content and features in Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="ab67f-126">Модули задач</span><span class="sxs-lookup"><span data-stu-id="ab67f-126">Task modules</span></span>

<span data-ttu-id="ab67f-127">Модуль задач — это модуль всплывающих модулей, который можно запускать с вкладки. На странице контента можно использовать модули задач для отображения форм для сбора дополнительных сведений, отображения сведений о элементе в списке или для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="ab67f-127">A task module is a modal pop-up experience that you can trigger from your tab. In a content page, you can use task modules to present forms for gathering additional information, displaying the details of an item in a list, or presenting the user with additional information.</span></span> <span data-ttu-id="ab67f-128">Сами модули задач могут быть дополнительными страницами контента или полностью создаваться с помощью адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="ab67f-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="ab67f-129">Дополнительные сведения см. в [таблицах с использованием модулей задач.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="ab67f-129">For more information, see [using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

### <a name="valid-domains"></a><span data-ttu-id="ab67f-130">Допустимые домены</span><span class="sxs-lookup"><span data-stu-id="ab67f-130">Valid domains</span></span>

<span data-ttu-id="ab67f-131">Убедитесь, что все URL-домены, используемые в вкладке, включены в массив `validDomains` [манифеста.](~/concepts/build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="ab67f-131">Ensure that all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="ab67f-132">Дополнительные сведения см. в справке по схеме манифеста [validDomains.](~/resources/schema/manifest-schema.md#validdomains)</span><span class="sxs-lookup"><span data-stu-id="ab67f-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span>

> [!NOTE]
> <span data-ttu-id="ab67f-133">Основные функции вкладки существуют в Teams, а не за пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="ab67f-133">The core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="ab67f-134">Показать индикатор загрузки</span><span class="sxs-lookup"><span data-stu-id="ab67f-134">Show a native loading indicator</span></span>

<span data-ttu-id="ab67f-135">Начиная с [схемы манифеста v1.7,](../../../resources/schema/manifest-schema.md)можно предоставить [индикатор](../../../resources/schema/manifest-schema.md#showloadingindicator)загрузки.</span><span class="sxs-lookup"><span data-stu-id="ab67f-135">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator).</span></span> <span data-ttu-id="ab67f-136">Например, страница [контента вкладок,](#integrate-your-code-with-teams) [страница конфигурации,](configuration-page.md)страница [удаления](removal-page.md)и модули [задач на вкладке](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="ab67f-136">For example, [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md), and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="ab67f-137">Поведение мобильных клиентов не настраивается с помощью свойства индикатора загрузки.</span><span class="sxs-lookup"><span data-stu-id="ab67f-137">The behavior on mobile clients is not configurable through the native loading indicator property.</span></span> <span data-ttu-id="ab67f-138">Мобильные клиенты по умолчанию показывают этот индикатор на страницах контента и модулях задач на основе iframe.</span><span class="sxs-lookup"><span data-stu-id="ab67f-138">Mobile clients show this indicator by default across content pages and iframe-based task modules.</span></span> <span data-ttu-id="ab67f-139">Этот индикатор на мобильном телефоне отображается при запросе на извлечение контента и его отклонять сразу же после завершения запроса.</span><span class="sxs-lookup"><span data-stu-id="ab67f-139">This indicator on mobile is shown when a request is made to fetch content and gets dismissed as soon as the request gets completed.</span></span>

<span data-ttu-id="ab67f-140">Если вы указываете в манифесте приложения, то все страницы конфигурации вкладок, контента и удаления и все модули задач на основе iframe должны следовать `showLoadingIndicator : true`  следующим шагам:</span><span class="sxs-lookup"><span data-stu-id="ab67f-140">If you indicate `showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow these steps:</span></span>

<span data-ttu-id="ab67f-141">**Показать индикатор загрузки**</span><span class="sxs-lookup"><span data-stu-id="ab67f-141">**To show the loading indicator**</span></span>

1. <span data-ttu-id="ab67f-142">Добавьте `"showLoadingIndicator": true` в манифест.</span><span class="sxs-lookup"><span data-stu-id="ab67f-142">Add `"showLoadingIndicator": true` to your manifest.</span></span>
1. <span data-ttu-id="ab67f-143">вызова метода `microsoftTeams.initialize();`;</span><span class="sxs-lookup"><span data-stu-id="ab67f-143">Call `microsoftTeams.initialize();`.</span></span>
1. <span data-ttu-id="ab67f-144">В качестве **обязательного** шага позвоните, чтобы уведомить Teams, что ваше приложение `microsoftTeams.appInitialization.notifySuccess()` успешно загружено.</span><span class="sxs-lookup"><span data-stu-id="ab67f-144">As a **mandatory** step, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="ab67f-145">Teams затем скрывает индикатор загрузки, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="ab67f-145">Teams then hides the loading indicator, if applicable.</span></span> <span data-ttu-id="ab67f-146">Если не вызвано в течение 30 секунд, предполагается, что ваше приложение ото времени и появится экран ошибок с параметром `notifySuccess`  повторной проверки.</span><span class="sxs-lookup"><span data-stu-id="ab67f-146">If `notifySuccess`  is not called within 30 seconds, it is assumed that your app timed out and an error screen with a retry option appears.</span></span>
1. <span data-ttu-id="ab67f-147">**Необязательно,** если вы готовы печатать на экране и хотите лениво загрузить остальную часть контента приложения, вы можете вручную скрыть индикатор загрузки, `microsoftTeams.appInitialization.notifyAppLoaded();` позвонив.</span><span class="sxs-lookup"><span data-stu-id="ab67f-147">**Optionally**, if you are ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`.</span></span>
1. <span data-ttu-id="ab67f-148">Если приложение не загружается, вы можете позвонить, чтобы `microsoftTeams.appInitialization.notifyFailure(reason);` Teams, что произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="ab67f-148">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="ab67f-149">Экран ошибки отображается пользователю.</span><span class="sxs-lookup"><span data-stu-id="ab67f-149">An error screen is shown to the user.</span></span> <span data-ttu-id="ab67f-150">В следующем коде приводится пример причин отказа приложения:</span><span class="sxs-lookup"><span data-stu-id="ab67f-150">The following code provides an example of application failure reasons:</span></span>

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="see-also"></a><span data-ttu-id="ab67f-151">См. также</span><span class="sxs-lookup"><span data-stu-id="ab67f-151">See also</span></span>

* [<span data-ttu-id="ab67f-152">Teams вкладки</span><span class="sxs-lookup"><span data-stu-id="ab67f-152">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="ab67f-153">Создание личной вкладки</span><span class="sxs-lookup"><span data-stu-id="ab67f-153">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="ab67f-154">Создание вкладки канала или группы</span><span class="sxs-lookup"><span data-stu-id="ab67f-154">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="ab67f-155">Создать страницу контента</span><span class="sxs-lookup"><span data-stu-id="ab67f-155">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="next-step"></a><span data-ttu-id="ab67f-156">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="ab67f-156">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab67f-157">Создать страницу конфигурации</span><span class="sxs-lookup"><span data-stu-id="ab67f-157">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
