---
title: Создать страницу контента
author: laujan
description: создание страницы контента
keywords: группы вкладок группового канала, настраиваемые статическими
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 619ca1079fcdb5a44eec2fa63d6687a0eb65cd4d
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479874"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="2fd93-104">Создание страницы контента для вкладки</span><span class="sxs-lookup"><span data-stu-id="2fd93-104">Create a content page for your tab</span></span>

<span data-ttu-id="2fd93-105">Страница контента — это веб-страница, отрисовка в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="2fd93-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="2fd93-106">Как правило, это часть:</span><span class="sxs-lookup"><span data-stu-id="2fd93-106">Typically these are part of:</span></span>

* <span data-ttu-id="2fd93-107">Настраиваемая вкладка с личным охватом . В этом случае страница контента является первой страницей, с которой сталкивается пользователь.</span><span class="sxs-lookup"><span data-stu-id="2fd93-107">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="2fd93-108">Настраиваемая вкладка канал/группа . После того, как пользователь наберет и настроит вкладку в соответствующем контексте, отображается страница контента.</span><span class="sxs-lookup"><span data-stu-id="2fd93-108">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="2fd93-109">Модуль [задач](~/task-modules-and-cards/what-are-task-modules.md) — вы можете создать страницу контента и встраить ее в веб-просмотр внутри модуля задач.</span><span class="sxs-lookup"><span data-stu-id="2fd93-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="2fd93-110">Страница будет отрисовка в всплывающее в моду.</span><span class="sxs-lookup"><span data-stu-id="2fd93-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="2fd93-111">Эта статья посвящена использованию страниц контента в качестве вкладок; однако большинство указаний здесь будет применяться независимо от того, как страница контента будет представлена конечному пользователю.</span><span class="sxs-lookup"><span data-stu-id="2fd93-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="2fd93-112">Рекомендации по контенту и стилю вкладок</span><span class="sxs-lookup"><span data-stu-id="2fd93-112">Tab content and style guidelines</span></span>

<span data-ttu-id="2fd93-113">Общая цель вкладки должна быть в том, чтобы предоставить доступ к содержательному и привлекательному контенту, который имеет практическое значение и очевидная цель.</span><span class="sxs-lookup"><span data-stu-id="2fd93-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="2fd93-114">Это не означает, что вам следует отойть от приятного стиля, но следует сосредоточиться на минимизации беспорядка, сделав дизайн вкладки чистым, интуитивно понятным и захватывающим контентом.</span><span class="sxs-lookup"><span data-stu-id="2fd93-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="2fd93-115">Просмотр [контента и бесед, все это одновременно](~/tabs/design/tabs.md) с помощью вкладок и руководства по процессу утверждения приложений Microsoft [Teams](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span><span class="sxs-lookup"><span data-stu-id="2fd93-115">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="2fd93-116">Интеграция кода с Teams</span><span class="sxs-lookup"><span data-stu-id="2fd93-116">Integrate your code with Teams</span></span>

<span data-ttu-id="2fd93-117">Для отображения страницы в Teams необходимо включить [SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) клиента Microsoft Teams JavaScript и включить вызов после загрузки `microsoftTeams.initialize()` страницы.</span><span class="sxs-lookup"><span data-stu-id="2fd93-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="2fd93-118">Таким образом ваша страница и клиент Teams общаются:</span><span class="sxs-lookup"><span data-stu-id="2fd93-118">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="2fd93-119">Доступ к дополнительному контенту</span><span class="sxs-lookup"><span data-stu-id="2fd93-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="2fd93-120">Использование SDK для взаимодействия с Teams</span><span class="sxs-lookup"><span data-stu-id="2fd93-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="2fd93-121">Клиент [Teams JavaScript SDK предоставляет](~/tabs/how-to/using-teams-client-sdk.md) множество дополнительных функций, которые могут оказаться полезными при разработке страницы контента.</span><span class="sxs-lookup"><span data-stu-id="2fd93-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="2fd93-122">Прямые ссылки</span><span class="sxs-lookup"><span data-stu-id="2fd93-122">Deep links</span></span>

<span data-ttu-id="2fd93-123">Можно создавать глубокие ссылки на сущности в Teams.</span><span class="sxs-lookup"><span data-stu-id="2fd93-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="2fd93-124">Как правило, они используются для создания ссылок, которые переходят к содержимому и сведениям в вкладке. См. в этой ссылке Создание глубоких ссылок на контент [и функции в Microsoft Teams.](~/concepts/build-and-test/deep-links.md)</span><span class="sxs-lookup"><span data-stu-id="2fd93-124">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="2fd93-125">Модули задач</span><span class="sxs-lookup"><span data-stu-id="2fd93-125">Task Modules</span></span>

<span data-ttu-id="2fd93-126">Модуль задач — это модуль, похожий на всплывающий модуль, который можно запускать с вкладки. Обычно на странице контента не нужно перемещаться по пользователю через несколько страниц.</span><span class="sxs-lookup"><span data-stu-id="2fd93-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="2fd93-127">Вместо этого вы будете использовать модули задач для отображения форм для сбора дополнительных сведений, отображения сведений о элементе в списке или в любое другое время, когда необходимо представить пользователю дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="2fd93-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="2fd93-128">Сами модули задач могут быть дополнительными страницами контента или полностью создаваться с помощью адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="2fd93-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="2fd93-129">Дополнительные сведения см. [в рубке Использование](~/task-modules-and-cards/task-modules/task-modules-tabs.md) модулей задач на вкладке.</span><span class="sxs-lookup"><span data-stu-id="2fd93-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="2fd93-130">Допустимые домены</span><span class="sxs-lookup"><span data-stu-id="2fd93-130">Valid Domains</span></span>

<span data-ttu-id="2fd93-131">Убедитесь, что все URL-домены, используемые в вкладке, включены в массив `validDomains` [манифеста.](~/concepts/build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="2fd93-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="2fd93-132">Дополнительные сведения см. в справке по схеме манифеста [validDomains.](~/resources/schema/manifest-schema.md#validdomains)</span><span class="sxs-lookup"><span data-stu-id="2fd93-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="2fd93-133">Однако следует помнить, что основные функции вкладки существуют в Teams, а не за пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="2fd93-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="reorder-static-personal-tabs"></a><span data-ttu-id="2fd93-134">Reorder static personal tabs</span><span class="sxs-lookup"><span data-stu-id="2fd93-134">Reorder static personal tabs</span></span>

<span data-ttu-id="2fd93-135">Начиная с манифеста версии 1.7, разработчики могут изменить все вкладки в своем личном приложении.</span><span class="sxs-lookup"><span data-stu-id="2fd93-135">Starting with manifest version 1.7, developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="2fd93-136">В частности, разработчик может  переместить вкладку чата бота, которая всегда по умолчанию, в первую позицию, в любом месте в личном загонах вкладки приложения.</span><span class="sxs-lookup"><span data-stu-id="2fd93-136">In particular, a developer can move the *bot chat* tab, which always defaults to the first position, anywhere in the personal app tab header.</span></span> <span data-ttu-id="2fd93-137">Мы задекларировали два зарезервированных ключевые слова, *беседы* и *около*.</span><span class="sxs-lookup"><span data-stu-id="2fd93-137">We’ve declared two reserved tab entityId keywords, *conversations* and *about*.</span></span>

<span data-ttu-id="2fd93-138">Если вы создаете бот с *личной* областью, он по умолчанию будет показываться в первой позиции вкладки в личном приложении.</span><span class="sxs-lookup"><span data-stu-id="2fd93-138">If you create a bot with a *personal* scope, it will show up in the first tab position in a personal app by default.</span></span> <span data-ttu-id="2fd93-139">Если вы хотите переместить его в другую позицию, необходимо добавить статичный объект вкладки в манифест с зарезервированным ключевым словом , *беседы*.</span><span class="sxs-lookup"><span data-stu-id="2fd93-139">If you wish to move it to another position, you must add a static tab object to your manifest with the reserved keyword, *conversations*.</span></span> <span data-ttu-id="2fd93-140">Вкладка *беседы* отображается на веб-сайте или на рабочем столе в зависимости от того, где вы добавляете вкладку *беседы* в `staticTabs` массиве.</span><span class="sxs-lookup"><span data-stu-id="2fd93-140">The *conversation* tab appears on web or desktop based on where you add the *conversation* tab in the `staticTabs` array.</span></span> 

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

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="2fd93-141">Показать индикатор загрузки</span><span class="sxs-lookup"><span data-stu-id="2fd93-141">Show a native loading indicator</span></span>

<span data-ttu-id="2fd93-142">Начиная с схемы манифеста [v1.7,](../../../resources/schema/manifest-schema.md)вы можете предоставить собственный индикатор загрузки везде, где ваш веб-контент загружается в Teams, [например,](#integrate-your-code-with-teams)страницу контента вкладок, страницу конфигурации, страницу удаления и модули задач на вкладке [.](../../../task-modules-and-cards/task-modules/task-modules-tabs.md) [](../../../resources/schema/manifest-schema.md#showloadingindicator) [](configuration-page.md) [](removal-page.md)</span><span class="sxs-lookup"><span data-stu-id="2fd93-142">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams, e.g., [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md) and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> 1. <span data-ttu-id="2fd93-143">На мобильных устройствах еще не поддерживается индикатор загрузки.</span><span class="sxs-lookup"><span data-stu-id="2fd93-143">The native loading indicator is not yet supported on mobile devices.</span></span>
> 2. <span data-ttu-id="2fd93-144">Если вы указываете в манифесте приложения, то все страницы конфигурации вкладок, контента и удаления и все модули задач на основе iframe должны следовать обязательному протоколу  `"showLoadingIndicator : true`  ниже:</span><span class="sxs-lookup"><span data-stu-id="2fd93-144">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>


1. <span data-ttu-id="2fd93-145">Чтобы показать индикатор загрузки, добавьте `"showLoadingIndicator": true` в манифест.</span><span class="sxs-lookup"><span data-stu-id="2fd93-145">To show the loading indicator, add `"showLoadingIndicator": true` to your manifest.</span></span> 
2. <span data-ttu-id="2fd93-146">Не забудьте `microsoftTeams.initialize();` позвонить.</span><span class="sxs-lookup"><span data-stu-id="2fd93-146">Remember to call `microsoftTeams.initialize();`.</span></span>
3. <span data-ttu-id="2fd93-147">**Необязательное поле**.</span><span class="sxs-lookup"><span data-stu-id="2fd93-147">**Optional**.</span></span> <span data-ttu-id="2fd93-148">Если вы готовы печатать на экране и хотите полениться загрузить остальную часть контента приложения, вы можете вручную скрыть индикатор загрузки, позвонив `microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="2fd93-148">If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
4. <span data-ttu-id="2fd93-149">**Обязательный**.</span><span class="sxs-lookup"><span data-stu-id="2fd93-149">**Mandatory**.</span></span> <span data-ttu-id="2fd93-150">Наконец, `microsoftTeams.appInitialization.notifySuccess()` позвоните, чтобы уведомить Teams об успешной загрузке приложения.</span><span class="sxs-lookup"><span data-stu-id="2fd93-150">Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="2fd93-151">Затем команды будут скрывать индикатор загрузки, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="2fd93-151">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="2fd93-152">Если не будет вызвано в течение 30 секунд, предполагается, что ваше приложение будет ото времени и появится экран ошибки с параметром  `notifySuccess`  повторной проверки.</span><span class="sxs-lookup"><span data-stu-id="2fd93-152">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
5. <span data-ttu-id="2fd93-153">Если приложение не загружается, вы можете позвонить, `microsoftTeams.appInitialization.notifyFailure(reason);` чтобы команд знали, что произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="2fd93-153">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="2fd93-154">Затем пользователю будет показан экран ошибки:</span><span class="sxs-lookup"><span data-stu-id="2fd93-154">An error screen will then be shown to the user:</span></span>

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
