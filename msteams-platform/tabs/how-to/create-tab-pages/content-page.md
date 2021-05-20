---
title: Создать страницу контента
author: laujan
description: как создать страницу содержимого
keywords: группы вкладок групповой канал настраиваемый статический
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 136160cb9154d62be40d8e29075ac1fc86135a6b
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566679"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="e92cc-104">Создание страницы содержимого для вкладки</span><span class="sxs-lookup"><span data-stu-id="e92cc-104">Create a content page for your tab</span></span>

<span data-ttu-id="e92cc-105">Страница содержимого – это веб-страница, которая отображается в Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="e92cc-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="e92cc-106">Как правило, они являются частью:</span><span class="sxs-lookup"><span data-stu-id="e92cc-106">Typically these are part of:</span></span>

* <span data-ttu-id="e92cc-107">Пользовательская вкладка с личным прицелом: В данном случае страница содержимого является первой страницей, с которую сталкивается пользователь.</span><span class="sxs-lookup"><span data-stu-id="e92cc-107">A personal-scoped custom tab: In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="e92cc-108">Пользовательская вкладка канала/группы: После того, как пользователь прикрепляет и настраивает вкладку в соответствующем контексте, отображается страница содержимого.</span><span class="sxs-lookup"><span data-stu-id="e92cc-108">A channel/group custom tab: After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="e92cc-109">Модуль [задачи:](~/task-modules-and-cards/what-are-task-modules.md)Вы можете создать страницу содержимого и встроить ее в веб-просмотр внутри модуля задач.</span><span class="sxs-lookup"><span data-stu-id="e92cc-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md): You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="e92cc-110">Страница будет отрисована внутри модального всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="e92cc-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="e92cc-111">Эта статья специфична для использования страниц содержимого в качестве вкладок; однако большинство рекомендаций здесь будет применяться независимо от того, как страница содержимого представлена конечному пользователю.</span><span class="sxs-lookup"><span data-stu-id="e92cc-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-design-guidelines"></a><span data-ttu-id="e92cc-112">Рекомендации по содержанию и дизайну вкладок</span><span class="sxs-lookup"><span data-stu-id="e92cc-112">Tab content and design guidelines</span></span>

<span data-ttu-id="e92cc-113">Общая цель вашей вкладки должна заключаться в предоставлении доступа к содержательному и привлекательному контенту, который имеет практическую ценность и очевидную цель.</span><span class="sxs-lookup"><span data-stu-id="e92cc-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="e92cc-114">Это не означает, что вы должны отказаться от приятного стиля, но вы должны сосредоточиться на минимизации беспорядка, сделав ваш дизайн вкладок чистым, навигация интуитивно понятным, и содержание погружения.</span><span class="sxs-lookup"><span data-stu-id="e92cc-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span>

<span data-ttu-id="e92cc-115">Для получения дополнительной информации [можно просмотреть руководящие принципы проектирования](~/tabs/design/tabs.md) [вкладок и Microsoft Teams рекомендации по проверке магазина](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)</span><span class="sxs-lookup"><span data-stu-id="e92cc-115">For more information, see the [tab design guidelines](~/tabs/design/tabs.md) and [Microsoft Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="e92cc-116">Интегрируйте свой код с Teams</span><span class="sxs-lookup"><span data-stu-id="e92cc-116">Integrate your code with Teams</span></span>

<span data-ttu-id="e92cc-117">Для отображения страницы в Teams вы должны включить [Microsoft Teams JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и включить вызов `microsoftTeams.initialize()` после загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="e92cc-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="e92cc-118">Вот как ваша страница и Teams клиент общаться:</span><span class="sxs-lookup"><span data-stu-id="e92cc-118">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="e92cc-119">Доступ к дополнительному контенту</span><span class="sxs-lookup"><span data-stu-id="e92cc-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="e92cc-120">Использование SDK для взаимодействия с Teams</span><span class="sxs-lookup"><span data-stu-id="e92cc-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="e92cc-121">Клиент [Teams JavaScript SDK предоставляет множество дополнительных](~/tabs/how-to/using-teams-client-sdk.md) функций, которые могут оказаться полезными при разработке страницы содержимого.</span><span class="sxs-lookup"><span data-stu-id="e92cc-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="e92cc-122">Прямые ссылки</span><span class="sxs-lookup"><span data-stu-id="e92cc-122">Deep links</span></span>

<span data-ttu-id="e92cc-123">Вы можете создать глубокие ссылки на сущности в Teams.</span><span class="sxs-lookup"><span data-stu-id="e92cc-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="e92cc-124">Как правило, они используются для создания ссылок, которые перемещаются по содержимому и информации в вашей вкладке. Для получения дополнительной информации [см. Создайте глубокие ссылки на содержание и функции в Microsoft Teams.](~/concepts/build-and-test/deep-links.md)</span><span class="sxs-lookup"><span data-stu-id="e92cc-124">Typically, these are used to create links that navigate to content and information within your tab. For more information, see [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="e92cc-125">Модули задач</span><span class="sxs-lookup"><span data-stu-id="e92cc-125">Task Modules</span></span>

<span data-ttu-id="e92cc-126">Модуль задачи — это модальный всплывающий опыт, который можно вызвать из вкладки. Обычно на странице содержимого вы не хотите перемещаться по нескольким страницам пользователя.</span><span class="sxs-lookup"><span data-stu-id="e92cc-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="e92cc-127">Вместо этого вы будете использовать модули задач для представления форм для сбора дополнительной информации, отображения деталей элемента в списке или в любое другое время, необходимое для представления пользователю дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="e92cc-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="e92cc-128">Сами модули задач могут быть дополнительными страницами содержимого или полностью созданными с помощью адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="e92cc-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="e92cc-129">Для [получения полной информации можно использовать модули задач](~/task-modules-and-cards/task-modules/task-modules-tabs.md) во вкладок.</span><span class="sxs-lookup"><span data-stu-id="e92cc-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="e92cc-130">Действительные домены</span><span class="sxs-lookup"><span data-stu-id="e92cc-130">Valid Domains</span></span>

<span data-ttu-id="e92cc-131">Убедитесь, что все домены URL, используемые в ваших вкладок, включены в `validDomains` массив в вашем [манифесте.](~/concepts/build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="e92cc-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="e92cc-132">Для получения дополнительной информации [см.](~/resources/schema/manifest-schema.md#validdomains)</span><span class="sxs-lookup"><span data-stu-id="e92cc-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="e92cc-133">Однако помните, что основная функциональность вкладки существует в Teams, а не за ее пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="e92cc-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="reorder-static-personal-tabs"></a><span data-ttu-id="e92cc-134">Перезаказ статических личных вкладок</span><span class="sxs-lookup"><span data-stu-id="e92cc-134">Reorder static personal tabs</span></span>

<span data-ttu-id="e92cc-135">Начиная с явной версии 1.7, разработчики могут изменить все вкладки в своем личном приложении.</span><span class="sxs-lookup"><span data-stu-id="e92cc-135">Starting with manifest version 1.7, developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="e92cc-136">В частности, разработчик может переместить вкладку *чата бота,* которая всегда по умолчанию, на первую позицию, в любом месте в заголовке вкладки личного приложения.</span><span class="sxs-lookup"><span data-stu-id="e92cc-136">In particular, a developer can move the *bot chat* tab, which always defaults to the first position, anywhere in the personal app tab header.</span></span> <span data-ttu-id="e92cc-137">Мы объявили две зарезервированные вкладки entityId ключевые *слова, разговоры* и *о*.</span><span class="sxs-lookup"><span data-stu-id="e92cc-137">We’ve declared two reserved tab entityId keywords, *conversations* and *about*.</span></span>

<span data-ttu-id="e92cc-138">Если вы создадите бота с *личной* областью, он появится в первой позиции вкладки в личном приложении по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e92cc-138">If you create a bot with a *personal* scope, it will show up in the first tab position in a personal app by default.</span></span> <span data-ttu-id="e92cc-139">Если вы хотите переместить его в другую позицию, вы должны добавить статический объект вкладки в ваш манифест с зарезервированным ключевым *словом, разговоры*.</span><span class="sxs-lookup"><span data-stu-id="e92cc-139">If you wish to move it to another position, you must add a static tab object to your manifest with the reserved keyword, *conversations*.</span></span> <span data-ttu-id="e92cc-140">Вкладка *беседы* отображается в Интернете или на рабочем столе в зависимости от того, где *вы добавляете вкладку* разговора в `staticTabs` массиве.</span><span class="sxs-lookup"><span data-stu-id="e92cc-140">The *conversation* tab appears on web or desktop based on where you add the *conversation* tab in the `staticTabs` array.</span></span> 

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

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="e92cc-141">Показать родной индикатор загрузки</span><span class="sxs-lookup"><span data-stu-id="e92cc-141">Show a native loading indicator</span></span>

<span data-ttu-id="e92cc-142">Начиная с [явной схемы v1.7, вы](../../../resources/schema/manifest-schema.md)можете предоставить [родной индикатор загрузки,](../../../resources/schema/manifest-schema.md#showloadingindicator) где ваш веб-контент загружается Teams.</span><span class="sxs-lookup"><span data-stu-id="e92cc-142">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams.</span></span> <span data-ttu-id="e92cc-143">Например, [страница содержимого вкладок,](#integrate-your-code-with-teams) [страница](configuration-page.md) [конфигурации, страница](removal-page.md)удаления и модули задач во [вкладок.](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="e92cc-143">For example, [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md), and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="e92cc-144">Поведение мобильных клиентов не настраивается через это явное свойство.</span><span class="sxs-lookup"><span data-stu-id="e92cc-144">The behavior on mobile clients is not configurable through this manifest property.</span></span> <span data-ttu-id="e92cc-145">Мобильные клиенты по умолчанию показывают родной индикатор загрузки на страницах контента и модули задач на основе iframe.</span><span class="sxs-lookup"><span data-stu-id="e92cc-145">Mobile clients show a native loading indicator by default across content pages and iframe-based task modules.</span></span> <span data-ttu-id="e92cc-146">Этот индикатор на мобильном телефоне отображается, когда запрос сделан для получения контента и отменяется, как только запрос будет завершен.</span><span class="sxs-lookup"><span data-stu-id="e92cc-146">This indicator on mobile is shown when a request is made to fetch content and gets dismissed as soon as the request gets completed.</span></span>
> * <span data-ttu-id="e92cc-147">Если вы  `"showLoadingIndicator : true`  указываете в манифесте приложения, то все страницы конфигурации вкладок, содержимое и удаление и все модули задач на основе iframe должны следовать обязательному протоколу ниже:</span><span class="sxs-lookup"><span data-stu-id="e92cc-147">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>

<span data-ttu-id="e92cc-148">**Показать индикатор загрузки**</span><span class="sxs-lookup"><span data-stu-id="e92cc-148">**To show the loading indicator**</span></span>

* <span data-ttu-id="e92cc-149">Добавьте `"showLoadingIndicator": true` к вашему манифесту.</span><span class="sxs-lookup"><span data-stu-id="e92cc-149">Add `"showLoadingIndicator": true` to your manifest.</span></span> 
* <span data-ttu-id="e92cc-150">Не забудьте позвонить `microsoftTeams.initialize();` .</span><span class="sxs-lookup"><span data-stu-id="e92cc-150">Remember to call `microsoftTeams.initialize();`.</span></span>
* <span data-ttu-id="e92cc-151">**Дополнительно**: Если вы готовы распечатать на экране и хотите лениво загрузить остальную часть содержимого приложения, вы можете вручную скрыть индикатор загрузки, позвонив `microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="e92cc-151">**Optional**: If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
* <span data-ttu-id="e92cc-152">**Обязательно:** Наконец, `microsoftTeams.appInitialization.notifySuccess()` позвоните, чтобы уведомить Teams, что ваше приложение успешно загружено.</span><span class="sxs-lookup"><span data-stu-id="e92cc-152">**Mandatory**: Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="e92cc-153">Teams скрыть индикатор загрузки, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="e92cc-153">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="e92cc-154">Если  `notifySuccess`  не вызывается в течение 30 секунд, предполагается, что ваше приложение приутяется и появится экран ошибок с опцией повторной попытки.</span><span class="sxs-lookup"><span data-stu-id="e92cc-154">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
* <span data-ttu-id="e92cc-155">Если приложение не загружается, вы можете позвонить, `microsoftTeams.appInitialization.notifyFailure(reason);` чтобы сообщить Teams, что произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="e92cc-155">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="e92cc-156">Экран ошибки будет показан пользователю:</span><span class="sxs-lookup"><span data-stu-id="e92cc-156">An error screen will then be shown to the user:</span></span>

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
