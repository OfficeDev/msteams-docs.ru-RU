---
title: Создать страницу контента
author: laujan
description: Создание страницы контента
keywords: вкладки Teams канал группы, настраиваемый статически
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 91a7d643d3a631610989e31eae14265cd725dbd0
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818908"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="8bd2a-104">Создание страницы контента для вкладки</span><span class="sxs-lookup"><span data-stu-id="8bd2a-104">Create a content page for your tab</span></span>

<span data-ttu-id="8bd2a-105">Страница контента — это веб-страница, которая отображается в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="8bd2a-106">Как правило, это часть:</span><span class="sxs-lookup"><span data-stu-id="8bd2a-106">Typically these are part of:</span></span>

* <span data-ttu-id="8bd2a-107">Настраиваемая настраиваемая вкладка — в этом экземпляре страница контента — это первая страница, с которой столкнулся пользователь.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-107">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="8bd2a-108">Настраиваемая вкладка канала/группы — после того как пользователь закрепляет и настраивает вкладку в соответствующем контексте, отображается страница содержимое.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-108">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="8bd2a-109">[Модуль задачи](~/task-modules-and-cards/what-are-task-modules.md) — вы можете создать страницу контента и внедрить ее как вебвиев в модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="8bd2a-110">Страница будет отображаться в модальном всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="8bd2a-111">Эта статья относится к использованию страниц содержимого в качестве вкладок; Тем не менее, в этом случае большинство рекомендаций применяется независимо от того, как страница контента представлена конечному пользователю.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="8bd2a-112">Рекомендации по содержимому и стилю вкладок</span><span class="sxs-lookup"><span data-stu-id="8bd2a-112">Tab content and style guidelines</span></span>

<span data-ttu-id="8bd2a-113">Общая цель вкладки должна обеспечивать доступ к осмысленному и привлекательному содержимому, которое имеет практичное значение и очевидное назначение.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="8bd2a-114">Это не означает, что вы должны быть более сои ненужным стилем, но следует сосредоточиться на минимизации несрочных данных, сделав Оформление вкладки четким, интуитивно понятную навигацию и содержимое.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="8bd2a-115">Просмотр [контента и бесед, всего одновременно с использованием вкладок](~/tabs/design/tabs.md) и [руководства по процессу утверждения приложений Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span><span class="sxs-lookup"><span data-stu-id="8bd2a-115">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="8bd2a-116">Интеграция кода с Teams</span><span class="sxs-lookup"><span data-stu-id="8bd2a-116">Integrate your code with Teams</span></span>

<span data-ttu-id="8bd2a-117">Чтобы страница отображалась в Teams, необходимо включить [клиентский пакет SDK Microsoft Teams для JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) и включить вызов `microsoftTeams.initialize()` после загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="8bd2a-118">Способ общения страницы и клиента teams:</span><span class="sxs-lookup"><span data-stu-id="8bd2a-118">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="8bd2a-119">Доступ к дополнительному содержимому</span><span class="sxs-lookup"><span data-stu-id="8bd2a-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="8bd2a-120">Использование пакета SDK для взаимодействия с Teams</span><span class="sxs-lookup"><span data-stu-id="8bd2a-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="8bd2a-121">[Клиентский пакет SDK для JavaScript для Teams](~/tabs/how-to/using-teams-client-sdk.md) предоставляет множество дополнительных функций, которые могут оказаться полезны при разработке контента.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developer your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="8bd2a-122">Прямые ссылки</span><span class="sxs-lookup"><span data-stu-id="8bd2a-122">Deep links</span></span>

<span data-ttu-id="8bd2a-123">Можно создавать глубокие ссылки на объекты в Teams.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="8bd2a-124">Как правило, они используются для создания ссылок для перехода к содержимому и информации на вкладке. Ознакомьтесь [со статьей Создание глубоких ссылок на контент и функции в Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span><span class="sxs-lookup"><span data-stu-id="8bd2a-124">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="8bd2a-125">Модули задач</span><span class="sxs-lookup"><span data-stu-id="8bd2a-125">Task Modules</span></span>

<span data-ttu-id="8bd2a-126">Модуль задачи — это модальный всплывающий интерфейс, который можно запустить на вкладке. Как правило, на странице содержимого не требуется перемещаться по нескольким страницам.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="8bd2a-127">Вместо этого вы будете использовать модули задач для предоставления форм для сбора дополнительных сведений, отображения сведений об элементе в списке или в любое другое время, необходимое для предоставления пользователю дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="8bd2a-128">Сами модули задач могут быть дополнительными страницами контента или полностью созданы с помощью адаптивных карточек.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="8bd2a-129">Полную информацию можно найти [в разделе Использование модулей задач на вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md) .</span><span class="sxs-lookup"><span data-stu-id="8bd2a-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="8bd2a-130">Допустимые домены</span><span class="sxs-lookup"><span data-stu-id="8bd2a-130">Valid Domains</span></span>

<span data-ttu-id="8bd2a-131">Убедитесь, что все домены URL-адресов, используемые в вкладках, включены в `validDomains` массив в [манифесте](~/concepts/build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="8bd2a-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="8bd2a-132">Дополнительные сведения см. в статье [валиддомаинс](~/resources/schema/manifest-schema.md#validdomains) в справочнике по схеме манифеста.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="8bd2a-133">Однако осторожным, что основные функциональные возможности вкладки находятся в Teams, а не вне Teams.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="8bd2a-134">Отображение индикатора загрузки в машинном коде</span><span class="sxs-lookup"><span data-stu-id="8bd2a-134">Show a native loading indicator</span></span>

<span data-ttu-id="8bd2a-135">Начиная с [схемы манифеста версии 1.7](../../../resources/schema/manifest-schema.md), вы можете предоставить [встроенный индикатор загрузки](../../../resources/schema/manifest-schema.md#showloadingindicator) везде, где веб-содержимое загружено в Teams, например, [Страница "содержимое вкладки"](#integrate-your-code-with-teams), [Страница конфигурации](configuration-page.md), страница [удаления](removal-page.md) и [модули задач на вкладках](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="8bd2a-135">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams, e.g., [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md) and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8bd2a-136">Если вы указываете  `"showLoadingIndicator : true`  в манифесте приложения, все страницы настройки вкладок, контента и удаления и все модули задач на основе IFRAME должны соответствовать обязательному протоколу ниже:</span><span class="sxs-lookup"><span data-stu-id="8bd2a-136">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>

1. <span data-ttu-id="8bd2a-137">Чтобы показать индикатор загрузки, добавьте `"showLoadingIndicator": true` его в манифест.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-137">To show the loading indicator, add `"showLoadingIndicator": true` to your manifest.</span></span> 
2. <span data-ttu-id="8bd2a-138">Не забудьте позвонить `microsoftTeams.initialize();` .</span><span class="sxs-lookup"><span data-stu-id="8bd2a-138">Remember to call `microsoftTeams.initialize();`.</span></span>
3. <span data-ttu-id="8bd2a-139">**Необязательный**параметр.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-139">**Optional**.</span></span> <span data-ttu-id="8bd2a-140">Если вы готовы к печати на экране и хотите выполнить отложенную загрузку оставшейся части содержимого приложения, можно вручную скрыть индикатор загрузки, вызвав `microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="8bd2a-140">If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
4. <span data-ttu-id="8bd2a-141">**Обязательный**параметр.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-141">**Mandatory**.</span></span> <span data-ttu-id="8bd2a-142">Наконец, вызовите `microsoftTeams.appInitialization.notifySuccess()` Teams, чтобы уведомить Teams о том, что приложение успешно загружено.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-142">Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="8bd2a-143">Затем команды скрывают индикатор загрузки, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-143">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="8bd2a-144">Если оно  `notifySuccess`  не вызвано в течение 30 секунд, будет считаться, что время ожидания вашего приложения истекло, и появится экран с сообщением об ошибке с параметром Retry.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-144">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
5. <span data-ttu-id="8bd2a-145">Если приложение не удается загрузить, вы можете позвонить, `microsoftTeams.appInitialization.notifyFailure(reason);` чтобы разрешить Teams знать об ошибке.</span><span class="sxs-lookup"><span data-stu-id="8bd2a-145">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="8bd2a-146">Затем пользователю будет показан экран ошибки:</span><span class="sxs-lookup"><span data-stu-id="8bd2a-146">An error screen will then be shown to the user:</span></span>

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
