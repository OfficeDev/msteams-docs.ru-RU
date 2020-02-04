---
title: Создание страницы контента
author: laujan
description: ''
keywords: вкладки Teams канал группы, настраиваемый статически
ms.topic: conceptual
ms.author: v-laujan
ms.openlocfilehash: ac85e000c9bdaebf28cb33143a7c82a348d3771e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675418"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="1e8a6-103">Создание страницы контента для вкладки</span><span class="sxs-lookup"><span data-stu-id="1e8a6-103">Create a content page for your tab</span></span>

<span data-ttu-id="1e8a6-104">Страница контента — это веб-страница, которая отображается в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-104">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="1e8a6-105">Как правило, это часть:</span><span class="sxs-lookup"><span data-stu-id="1e8a6-105">Typically these are part of:</span></span>

* <span data-ttu-id="1e8a6-106">Настраиваемая настраиваемая вкладка — в этом экземпляре страница контента — это первая страница, с которой столкнулся пользователь.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-106">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="1e8a6-107">Настраиваемая вкладка канала/группы — после того как пользователь закрепляет и настраивает вкладку в соответствующем контексте, отображается страница содержимое.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-107">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="1e8a6-108">[Модуль задачи](~/task-modules-and-cards/what-are-task-modules.md) — вы можете создать страницу контента и внедрить ее как вебвиев в модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-108">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="1e8a6-109">Страница будет отображаться в модальном всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-109">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="1e8a6-110">Эта статья относится к использованию страниц содержимого в качестве вкладок; Тем не менее, в этом случае большинство рекомендаций применяется независимо от того, как страница контента представлена конечному пользователю.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-110">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="1e8a6-111">Рекомендации по содержимому и стилю вкладок</span><span class="sxs-lookup"><span data-stu-id="1e8a6-111">Tab content and style guidelines</span></span>

<span data-ttu-id="1e8a6-112">Общая цель вкладки должна обеспечивать доступ к осмысленному и привлекательному содержимому, которое имеет практичное значение и очевидное назначение.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-112">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="1e8a6-113">Это не означает, что вы должны быть более сои ненужным стилем, но следует сосредоточиться на минимизации несрочных данных, сделав Оформление вкладки четким, интуитивно понятную навигацию и содержимое.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-113">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="1e8a6-114">Просмотр [контента и бесед, всего одновременно с использованием вкладок](~/tabs/design/tabs.md) и [руководства по процессу утверждения приложений Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span><span class="sxs-lookup"><span data-stu-id="1e8a6-114">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="1e8a6-115">Интеграция кода с Teams</span><span class="sxs-lookup"><span data-stu-id="1e8a6-115">Integrate your code with Teams</span></span>

<span data-ttu-id="1e8a6-116">Чтобы страница отображалась в Teams, необходимо включить [клиентский пакет SDK Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) для `microsoftTeams.initialize()` JavaScript и включить вызов после загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-116">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="1e8a6-117">Способ общения страницы и клиента teams:</span><span class="sxs-lookup"><span data-stu-id="1e8a6-117">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="1e8a6-118">Доступ к дополнительному содержимому</span><span class="sxs-lookup"><span data-stu-id="1e8a6-118">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="1e8a6-119">Использование пакета SDK для взаимодействия с Teams</span><span class="sxs-lookup"><span data-stu-id="1e8a6-119">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="1e8a6-120">[Клиентский пакет SDK для JavaScript для Teams](~/tabs/how-to/using-teams-client-sdk.md) предоставляет множество дополнительных функций, которые могут оказаться полезны при разработке контента.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-120">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developer your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="1e8a6-121">Прямые ссылки</span><span class="sxs-lookup"><span data-stu-id="1e8a6-121">Deep links</span></span>

<span data-ttu-id="1e8a6-122">Можно создавать глубокие ссылки на объекты в Teams.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-122">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="1e8a6-123">Как правило, они используются для создания ссылок для перехода к содержимому и информации на вкладке. Ознакомьтесь [со статьей Создание глубоких ссылок на контент и функции в Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span><span class="sxs-lookup"><span data-stu-id="1e8a6-123">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="1e8a6-124">Модули задач</span><span class="sxs-lookup"><span data-stu-id="1e8a6-124">Task Modules</span></span>

<span data-ttu-id="1e8a6-125">Модуль задачи — это модальное всплывающее диалоговое окно, которое можно активировать с помощью вкладки. обычно на странице содержимого вы не хотите перемещаться по нескольким страницам.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-125">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="1e8a6-126">Вместо этого вы будете использовать модули задач для предоставления форм для сбора дополнительных сведений, отображения сведений об элементе в списке или в любое другое время, необходимое для предоставления пользователю дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-126">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="1e8a6-127">Сами модули задач могут быть дополнительными страницами контента или полностью созданы с помощью адаптивных карточек.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-127">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="1e8a6-128">Полную информацию можно найти [в разделе Использование модулей задач на вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md) .</span><span class="sxs-lookup"><span data-stu-id="1e8a6-128">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="1e8a6-129">Допустимые домены</span><span class="sxs-lookup"><span data-stu-id="1e8a6-129">Valid Domains</span></span>

<span data-ttu-id="1e8a6-130">Убедитесь, что все домены URL-адресов, используемые в вкладках `validDomains` , включены в массив в [манифесте](~/concepts/build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="1e8a6-130">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="1e8a6-131">Дополнительные сведения см. в статье [валиддомаинс](~/resources/schema/manifest-schema.md#validdomains) в справочнике по схеме манифеста.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-131">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="1e8a6-132">Однако осторожным, что основные функциональные возможности вкладки находятся в Teams, а не вне Teams.</span><span class="sxs-lookup"><span data-stu-id="1e8a6-132">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>
