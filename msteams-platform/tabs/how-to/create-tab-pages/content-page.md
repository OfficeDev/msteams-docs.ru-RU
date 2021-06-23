---
title: Создать страницу контента
author: surbhigupta
description: создание страницы контента
keywords: группы вкладок группового канала, настраиваемые статическими
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: abb073cee4a9417ee4a9f095acdbe18c5e6d7713
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068521"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="aa056-104">Создание страницы контента для вкладки</span><span class="sxs-lookup"><span data-stu-id="aa056-104">Create a content page for your tab</span></span>

<span data-ttu-id="aa056-105">Страница контента — это веб-страница, отрисовка в Teams клиенте.</span><span class="sxs-lookup"><span data-stu-id="aa056-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="aa056-106">Как правило, это часть:</span><span class="sxs-lookup"><span data-stu-id="aa056-106">Typically these are part of:</span></span>

* <span data-ttu-id="aa056-107">Настраиваемая вкладка с личным охватом. В этом случае страница контента является первой страницей, с которой сталкивается пользователь.</span><span class="sxs-lookup"><span data-stu-id="aa056-107">A personal-scoped custom tab: In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="aa056-108">Настраиваемая вкладка канал/группа. После того как пользователь задает и настроит вкладку в соответствующем контексте, отображается страница контента.</span><span class="sxs-lookup"><span data-stu-id="aa056-108">A channel/group custom tab: After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="aa056-109">Модуль [задач.](~/task-modules-and-cards/what-are-task-modules.md)Вы можете создать страницу контента и встраить ее в веб-просмотр внутри модуля задач.</span><span class="sxs-lookup"><span data-stu-id="aa056-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md): You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="aa056-110">Страница будет отрисовка в всплывающее в моду.</span><span class="sxs-lookup"><span data-stu-id="aa056-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="aa056-111">Эта статья посвящена использованию страниц контента в качестве вкладок; однако большинство указаний здесь будет применяться независимо от того, как страница контента будет представлена конечному пользователю.</span><span class="sxs-lookup"><span data-stu-id="aa056-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-design-guidelines"></a><span data-ttu-id="aa056-112">Рекомендации по контенту и дизайну вкладок</span><span class="sxs-lookup"><span data-stu-id="aa056-112">Tab content and design guidelines</span></span>

<span data-ttu-id="aa056-113">Общая цель вкладки должна быть в том, чтобы предоставить доступ к содержательному и привлекательному контенту, который имеет практическое значение и очевидная цель.</span><span class="sxs-lookup"><span data-stu-id="aa056-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="aa056-114">Это не означает, что вам следует отойть от приятного стиля, но следует сосредоточиться на минимизации беспорядка, сделав дизайн вкладки чистым, интуитивно понятным и захватывающим контентом.</span><span class="sxs-lookup"><span data-stu-id="aa056-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span>

<span data-ttu-id="aa056-115">Дополнительные сведения см. в [руководстве](~/tabs/design/tabs.md) по разработке вкладок [и рекомендациях по](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) проверке Microsoft Teams хранения</span><span class="sxs-lookup"><span data-stu-id="aa056-115">For more information, see the [tab design guidelines](~/tabs/design/tabs.md) and [Microsoft Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="aa056-116">Интеграция кода с Teams</span><span class="sxs-lookup"><span data-stu-id="aa056-116">Integrate your code with Teams</span></span>

<span data-ttu-id="aa056-117">Чтобы ваша страница отображалась в Teams, необходимо включить Microsoft Teams [клиента JavaScript sDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и включить вызов после загрузки `microsoftTeams.initialize()` страницы.</span><span class="sxs-lookup"><span data-stu-id="aa056-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="aa056-118">Таким образом ваша страница и клиент Teams:</span><span class="sxs-lookup"><span data-stu-id="aa056-118">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="aa056-119">Доступ к дополнительному контенту</span><span class="sxs-lookup"><span data-stu-id="aa056-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="aa056-120">Использование SDK для взаимодействия с Teams</span><span class="sxs-lookup"><span data-stu-id="aa056-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="aa056-121">Клиентская [Teams JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) предоставляет множество дополнительных функций, которые могут оказаться полезными при разработке страницы контента.</span><span class="sxs-lookup"><span data-stu-id="aa056-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="aa056-122">Прямые ссылки</span><span class="sxs-lookup"><span data-stu-id="aa056-122">Deep links</span></span>

<span data-ttu-id="aa056-123">Можно создавать глубокие ссылки на сущности в Teams.</span><span class="sxs-lookup"><span data-stu-id="aa056-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="aa056-124">Как правило, они используются для создания ссылок, которые переходят к содержимому и сведениям в вкладке. Дополнительные сведения см. в [материалах Create deep links to content and features in Microsoft Teams.](~/concepts/build-and-test/deep-links.md)</span><span class="sxs-lookup"><span data-stu-id="aa056-124">Typically, these are used to create links that navigate to content and information within your tab. For more information, see [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="aa056-125">Модули задач</span><span class="sxs-lookup"><span data-stu-id="aa056-125">Task Modules</span></span>

<span data-ttu-id="aa056-126">Модуль задач — это модуль, похожий на всплывающий модуль, который можно запускать с вкладки. Обычно на странице контента не нужно перемещаться по пользователю через несколько страниц.</span><span class="sxs-lookup"><span data-stu-id="aa056-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="aa056-127">Вместо этого вы будете использовать модули задач для отображения форм для сбора дополнительных сведений, отображения сведений о элементе в списке или в любое другое время, когда необходимо представить пользователю дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="aa056-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="aa056-128">Сами модули задач могут быть дополнительными страницами контента или полностью создаваться с помощью адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="aa056-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="aa056-129">Дополнительные сведения см. [в рубке Использование](~/task-modules-and-cards/task-modules/task-modules-tabs.md) модулей задач на вкладке.</span><span class="sxs-lookup"><span data-stu-id="aa056-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="aa056-130">Допустимые домены</span><span class="sxs-lookup"><span data-stu-id="aa056-130">Valid Domains</span></span>

<span data-ttu-id="aa056-131">Убедитесь, что все URL-домены, используемые в вкладке, включены в массив `validDomains` [манифеста.](~/concepts/build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="aa056-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="aa056-132">Дополнительные сведения см. в справке по схеме манифеста [validDomains.](~/resources/schema/manifest-schema.md#validdomains)</span><span class="sxs-lookup"><span data-stu-id="aa056-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="aa056-133">Однако следует помнить, что основные функции вкладки существуют в Teams, а не за пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="aa056-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="reorder-static-personal-tabs"></a><span data-ttu-id="aa056-134">Reorder static personal tabs</span><span class="sxs-lookup"><span data-stu-id="aa056-134">Reorder static personal tabs</span></span>

<span data-ttu-id="aa056-135">Начиная с манифеста версии 1.7, разработчики могут изменить все вкладки в своем личном приложении.</span><span class="sxs-lookup"><span data-stu-id="aa056-135">Starting with manifest version 1.7, developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="aa056-136">В частности, разработчик может  переместить вкладку чата бота, которая всегда по умолчанию, в первую позицию, в любом месте в личном загонах вкладки приложения.</span><span class="sxs-lookup"><span data-stu-id="aa056-136">In particular, a developer can move the *bot chat* tab, which always defaults to the first position, anywhere in the personal app tab header.</span></span> <span data-ttu-id="aa056-137">Мы задекларировали два зарезервированных ключевые слова, *беседы* и *около*.</span><span class="sxs-lookup"><span data-stu-id="aa056-137">We’ve declared two reserved tab entityId keywords, *conversations* and *about*.</span></span>

<span data-ttu-id="aa056-138">Если вы создаете бот с *личной* областью, он по умолчанию будет показываться в первой позиции вкладки в личном приложении.</span><span class="sxs-lookup"><span data-stu-id="aa056-138">If you create a bot with a *personal* scope, it will show up in the first tab position in a personal app by default.</span></span> <span data-ttu-id="aa056-139">Если вы хотите переместить его в другую позицию, необходимо добавить статичный объект вкладки в манифест с зарезервированным ключевым словом , *беседы*.</span><span class="sxs-lookup"><span data-stu-id="aa056-139">If you wish to move it to another position, you must add a static tab object to your manifest with the reserved keyword, *conversations*.</span></span> <span data-ttu-id="aa056-140">Вкладка *беседы* отображается на веб-сайте или на рабочем столе в зависимости от того, где вы добавляете вкладку *беседы* в `staticTabs` массиве.</span><span class="sxs-lookup"><span data-stu-id="aa056-140">The *conversation* tab appears on web or desktop based on where you add the *conversation* tab in the `staticTabs` array.</span></span> 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="aa056-141">Показать индикатор загрузки</span><span class="sxs-lookup"><span data-stu-id="aa056-141">Show a native loading indicator</span></span>

<span data-ttu-id="aa056-142">Начиная с [](../../../resources/schema/manifest-schema.md#showloadingindicator) [схемы манифеста v1.7,](../../../resources/schema/manifest-schema.md)вы можете предоставить индикатор загрузки, где бы веб-содержимое не загружалось в Teams.</span><span class="sxs-lookup"><span data-stu-id="aa056-142">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams.</span></span> <span data-ttu-id="aa056-143">Например, страница [контента вкладок,](#integrate-your-code-with-teams) [страница конфигурации,](configuration-page.md)страница [удаления](removal-page.md)и модули [задач на вкладке](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="aa056-143">For example, [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md), and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="aa056-144">Поведение мобильных клиентов не настраивается с помощью этого свойства манифеста.</span><span class="sxs-lookup"><span data-stu-id="aa056-144">The behavior on mobile clients is not configurable through this manifest property.</span></span> <span data-ttu-id="aa056-145">Мобильные клиенты показывают индикатор загрузки по умолчанию на страницах контента и модулях задач на основе iframe.</span><span class="sxs-lookup"><span data-stu-id="aa056-145">Mobile clients show a native loading indicator by default across content pages and iframe-based task modules.</span></span> <span data-ttu-id="aa056-146">Этот индикатор на мобильном телефоне отображается при запросе на извлечение контента и его отклонять сразу же после завершения запроса.</span><span class="sxs-lookup"><span data-stu-id="aa056-146">This indicator on mobile is shown when a request is made to fetch content and gets dismissed as soon as the request gets completed.</span></span>
> * <span data-ttu-id="aa056-147">Если вы указываете в манифесте приложения, то все страницы конфигурации вкладок, контента и удаления и все модули задач на основе iframe должны следовать обязательному протоколу  `"showLoadingIndicator : true`  ниже:</span><span class="sxs-lookup"><span data-stu-id="aa056-147">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>

<span data-ttu-id="aa056-148">**Показать индикатор загрузки**</span><span class="sxs-lookup"><span data-stu-id="aa056-148">**To show the loading indicator**</span></span>

* <span data-ttu-id="aa056-149">Добавьте `"showLoadingIndicator": true` в манифест.</span><span class="sxs-lookup"><span data-stu-id="aa056-149">Add `"showLoadingIndicator": true` to your manifest.</span></span> 
* <span data-ttu-id="aa056-150">Не забудьте `microsoftTeams.initialize();` позвонить.</span><span class="sxs-lookup"><span data-stu-id="aa056-150">Remember to call `microsoftTeams.initialize();`.</span></span>
* <span data-ttu-id="aa056-151">Необязательный. Если вы готовы печатать на экране и хотите полениться загрузить остальную часть контента приложения, вы можете вручную скрыть индикатор загрузки, позвонив`microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="aa056-151">**Optional**: If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
* <span data-ttu-id="aa056-152">**Обязательный:** Наконец, вызов, чтобы `microsoftTeams.appInitialization.notifySuccess()` Teams, что ваше приложение успешно загружено.</span><span class="sxs-lookup"><span data-stu-id="aa056-152">**Mandatory**: Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="aa056-153">Teams затем будет скрывать индикатор загрузки, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="aa056-153">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="aa056-154">Если не будет вызвано в течение 30 секунд, предполагается, что ваше приложение будет ото времени и появится экран ошибки с параметром  `notifySuccess`  повторной проверки.</span><span class="sxs-lookup"><span data-stu-id="aa056-154">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
* <span data-ttu-id="aa056-155">Если приложение не загружается, вы можете позвонить, чтобы `microsoftTeams.appInitialization.notifyFailure(reason);` Teams, что произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="aa056-155">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="aa056-156">Затем пользователю будет показан экран ошибки:</span><span class="sxs-lookup"><span data-stu-id="aa056-156">An error screen will then be shown to the user:</span></span>

    ```typescript
    ``
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```
    >
