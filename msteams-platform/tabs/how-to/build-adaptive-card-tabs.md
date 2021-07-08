---
title: Создание вкладок адаптивной карты
author: KirtiPereira
description: Создание вкладок с помощью адаптивных карт
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 5a66f49db3710885b926a7abce45ef858bf0b092
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328060"
---
# <a name="build-tabs-with-adaptive-cards"></a><span data-ttu-id="14a5f-103">Создание вкладок с использованием адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="14a5f-103">Build tabs with Adaptive Cards</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="14a5f-104">Эта функция находится в [общедоступных Developer Preview](~/resources/dev-preview/developer-preview-intro.md) поддерживается в настольных компьютерах и мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="14a5f-104">This feature is in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) and is supported in desktop and mobile.</span></span> <span data-ttu-id="14a5f-105">Поддержка в веб-браузере скоро.</span><span class="sxs-lookup"><span data-stu-id="14a5f-105">Support in the web browser is coming soon.</span></span>
> * <span data-ttu-id="14a5f-106">Вкладки с адаптивными картами в настоящее время поддерживаются только в качестве личных приложений.</span><span class="sxs-lookup"><span data-stu-id="14a5f-106">Tabs with Adaptive Cards are currently only supported as personal apps.</span></span>

<span data-ttu-id="14a5f-107">При разработке вкладки с помощью традиционного метода могут возникнуть такие проблемы, как соображения HTML и CSS, медленное время загрузки, ограничения iFrame, обслуживание и затраты серверов.</span><span class="sxs-lookup"><span data-stu-id="14a5f-107">When developing a tab using the traditional method, you might run into these issues, such as HTML and CSS considerations, slow load times, iFrame constraints, and server maintenance and costs.</span></span> <span data-ttu-id="14a5f-108">Адаптивные вкладки карты — это новый способ создания вкладок в Teams.</span><span class="sxs-lookup"><span data-stu-id="14a5f-108">Adaptive Card tabs is a new way to build tabs in Teams.</span></span> <span data-ttu-id="14a5f-109">Вместо встраив веб-контент в IFrame, вы можете отрисовки адаптивных карт на вкладку. В то время как передняя часть отрисовывана с помощью адаптивных карт, задний задаток будет работать с помощью бота.</span><span class="sxs-lookup"><span data-stu-id="14a5f-109">Instead of embedding web content in an IFrame, you can render Adaptive Cards to a tab. While the front-end is rendered with Adaptive Cards, the backend is powered by a bot.</span></span> <span data-ttu-id="14a5f-110">Бот отвечает за прием запросов и соответствующий ответ с помощью отрисовки адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="14a5f-110">The bot is responsible for accepting requests and responding appropriately with the Adaptive Card that is rendered.</span></span>

<span data-ttu-id="14a5f-111">Вы можете создавать вкладки с помощью готовых пользовательских интерфейсов (пользовательского интерфейса) Lego-блоков, которые выглядят и чувствуют себя родными на рабочем столе, в Интернете и на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="14a5f-111">You can build your tabs with ready-made user interface (UI) Lego-blocks that look and feel native on desktop, web, and mobile.</span></span> <span data-ttu-id="14a5f-112">В этой статье вы сможете понять изменения, необходимые для манифеста приложения, как запрашивает действия и отправляет сведения на вкладке с адаптивными картами, а также влияние на рабочий процесс модуля задач.</span><span class="sxs-lookup"><span data-stu-id="14a5f-112">This article helps you understand the changes required to be made to the app manifest, how the invoke activity requests and sends information in tab with Adaptive Cards, and the impact on the task module workflow.</span></span>

<span data-ttu-id="14a5f-113">На следующем изображении показаны вкладки сборки с адаптивными картами в настольных и мобильных устройствах:</span><span class="sxs-lookup"><span data-stu-id="14a5f-113">The following image depicts build tabs with Adaptive Cards in desktop and mobile:</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="Пример адаптивной карты, отрисовываемой на вкладке." border="false":::

## <a name="prerequisites"></a><span data-ttu-id="14a5f-115">Предварительные условия</span><span class="sxs-lookup"><span data-stu-id="14a5f-115">Prerequisites</span></span>

<span data-ttu-id="14a5f-116">Прежде чем приступить к созданию вкладок с помощью адаптивных карт, необходимо:</span><span class="sxs-lookup"><span data-stu-id="14a5f-116">Before you start using Adaptive Cards to build tabs, you must:</span></span>

* <span data-ttu-id="14a5f-117">Ознакомьтесь с разработкой [ботов,](../../bots/what-are-bots.md) [адаптивными](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)картами и модулями задач [в](../../task-modules-and-cards/task-modules/task-modules-bots.md) Teams.</span><span class="sxs-lookup"><span data-stu-id="14a5f-117">Be familiar with, [bot development](../../bots/what-are-bots.md), [Adaptive Cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards), and [task modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) in Teams.</span></span>
* <span data-ttu-id="14a5f-118">У вас есть бот, работающий в Teams для разработки.</span><span class="sxs-lookup"><span data-stu-id="14a5f-118">Have a bot running in Teams for your development.</span></span>
* <span data-ttu-id="14a5f-119">Будьте в [общедоступных Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="14a5f-119">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="changes-to-app-manifest"></a><span data-ttu-id="14a5f-120">Изменения манифеста приложений</span><span class="sxs-lookup"><span data-stu-id="14a5f-120">Changes to app manifest</span></span>

<span data-ttu-id="14a5f-121">Личные приложения, которые отрисовка вкладок должны включать `staticTabs` массив в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="14a5f-121">Personal apps that render tabs must include a `staticTabs` array in their app manifest.</span></span> <span data-ttu-id="14a5f-122">Вкладки адаптивной карты отрисовываться, когда `contentBotId` свойство предоставлено в `staticTab` определении.</span><span class="sxs-lookup"><span data-stu-id="14a5f-122">Adaptive Card tabs are rendered when the `contentBotId` property is provided in the `staticTab` definition.</span></span> <span data-ttu-id="14a5f-123">Статические определения вкладок должны содержать либо вкладку Адаптивная карточка, либо типичную хозяйную вкладку `contentBotId` `contentUrl` веб-контента.</span><span class="sxs-lookup"><span data-stu-id="14a5f-123">Static tab definitions must contain either a `contentBotId`, specifying an Adaptive Card tab or a `contentUrl`, specifying a typical hosted web content tab experience.</span></span>

> [!NOTE]
> <span data-ttu-id="14a5f-124">Свойство `contentBotId` в настоящее время доступно в манифестной версии 1.9 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="14a5f-124">The `contentBotId` property is currently available in manifest version 1.9 or later.</span></span>

<span data-ttu-id="14a5f-125">`contentBotId`Предобередим свойство вкладке Adaptive Card, с которую `botId` необходимо связаться.</span><span class="sxs-lookup"><span data-stu-id="14a5f-125">Provide the `contentBotId` property with the `botId` that the Adaptive Card tab must communicate with.</span></span> <span data-ttu-id="14a5f-126">Настроенная для вкладки Адаптивная карта отправляется в параметре каждого запроса на вызов и может использоваться для дифференцировать вкладки адаптивной карты, которые используются одним и тем же `entityId` `tabContext` ботом.</span><span class="sxs-lookup"><span data-stu-id="14a5f-126">The `entityId` configured for the Adaptive Card tab is sent in the `tabContext` parameter of each invoke request, and can be used to differentiate Adaptive Card Tabs that are powered by the same bot.</span></span> <span data-ttu-id="14a5f-127">Дополнительные сведения о других полях определения статических вкладок см. в [схеме манифеста.](../../resources/schema/manifest-schema.md#statictabs)</span><span class="sxs-lookup"><span data-stu-id="14a5f-127">For more information about other static tab definition fields, see [manifest schema](../../resources/schema/manifest-schema.md#statictabs).</span></span>

<span data-ttu-id="14a5f-128">Ниже приводится пример манифеста вкладки Адаптивная карта:</span><span class="sxs-lookup"><span data-stu-id="14a5f-128">Following is a sample Adaptive Card tab manifest:</span></span>

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "1.9",
  "id": "00000000-0000-0000-0000-000000000000",
  "version": "0.0.1",
  "packageName": "acprototype",
  "developer": {
    "name": "Contoso",
    "websiteUrl": "https://contoso.yourwebsite.com",
    "privacyUrl": "https://contoso.yourwebsite.com/privacy.html",
    "termsOfUseUrl": "https://contoso.yourwebsite.com/terms.html"
  },
  "name": {
    "short": "Contoso",
    "full": "Contoso Home"
  },
  "description": {
    "short": "Add short description here",
    "full": "Add full description here"
  },
  "icons": {
    "outline": "icon-outline.png",
    "color": "icon-color.png"
  },
  "accentColor": "#D85028",
  "configurableTabs": [],
  "staticTabs": [
    {
      "entityId": "homeTab",
      "name": "Home",
      "contentBotId": "00000000-0000-0000-0000-000000000000",
      "scopes": ["personal"]
    },
    {
      "entityId": "moreTab",
      "name": "More",
      "contentBotId": "00000000-0000-0000-0000-000000000000",
      "scopes": ["personal"]
    }
  ],
  "connectors": [],
  "composeExtensions": [],
  "permissions": ["identity", "messageTeamMembers"],
  "validDomains": [
    "contoso.yourwebsite.com",
    "token.botframework.com"
  ]
}
```

## <a name="invoke-activities"></a><span data-ttu-id="14a5f-129">Вызов действий</span><span class="sxs-lookup"><span data-stu-id="14a5f-129">Invoke activities</span></span>

<span data-ttu-id="14a5f-130">Связь между вкладкой Адаптивная карта и ботом делается с помощью `invoke` действий.</span><span class="sxs-lookup"><span data-stu-id="14a5f-130">Communication between your Adaptive Card tab and your bot is done through `invoke` activities.</span></span> <span data-ttu-id="14a5f-131">Каждое `invoke` действие имеет соответствующее **имя.**</span><span class="sxs-lookup"><span data-stu-id="14a5f-131">Each `invoke` activity has a corresponding **name**.</span></span> <span data-ttu-id="14a5f-132">Используйте имя каждого действия, чтобы различать каждый запрос.</span><span class="sxs-lookup"><span data-stu-id="14a5f-132">Use the name of each activity to differentiate each request.</span></span> <span data-ttu-id="14a5f-133">`tab/fetch` и `tab/submit` являются действиями, охватываемых в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="14a5f-133">`tab/fetch` and `tab/submit` are the activities covered in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="14a5f-134">Боты должны отправлять все ответы на [URL-адрес службы.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="14a5f-134">Bots need to send all the responses to [service URL](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true).</span></span> <span data-ttu-id="14a5f-135">URL-адрес службы получается в составе входящих `activity` полезной нагрузки.</span><span class="sxs-lookup"><span data-stu-id="14a5f-135">Service URL is received as part of incoming `activity` payload.</span></span>

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a><span data-ttu-id="14a5f-136">Извлечение адаптивной карты для отрисовки на вкладке</span><span class="sxs-lookup"><span data-stu-id="14a5f-136">Fetch Adaptive Card to render to a tab</span></span>

<span data-ttu-id="14a5f-137">`tab/fetch`это первый запрос на вызов, который ваш бот получает, когда пользователь открывает вкладку Адаптивная карта. Когда ваш бот получает запрос, он отправляет  вкладку продолжить ответ или ответ **auth вкладки.**</span><span class="sxs-lookup"><span data-stu-id="14a5f-137">`tab/fetch` is the first invoke request that your bot receives when a user opens an Adaptive Card tab. When your bot receives the request, it either sends a tab **continue** response or a tab **auth** response.</span></span>
<span data-ttu-id="14a5f-138">Продолжение **ответа** включает массив для **карт,** который отрисовывется вертикально на вкладку в порядке массива.</span><span class="sxs-lookup"><span data-stu-id="14a5f-138">The **continue** response includes an array for **cards**, which is rendered vertically to the tab in the order of the array.</span></span>

> [!NOTE]
> <span data-ttu-id="14a5f-139">Дополнительные сведения о **ответе auth** см. в [сайте проверки подлинности.](#authentication)</span><span class="sxs-lookup"><span data-stu-id="14a5f-139">For more information on **auth** response, see [authentication](#authentication).</span></span>

<span data-ttu-id="14a5f-140">В следующем коде приводится пример `tab/fetch` запроса и ответа:</span><span class="sxs-lookup"><span data-stu-id="14a5f-140">The following code provides examples of `tab/fetch` request and response:</span></span>

<span data-ttu-id="14a5f-141">**`tab/fetch` запрос**</span><span class="sxs-lookup"><span data-stu-id="14a5f-141">**`tab/fetch` request**</span></span>

```json
// tab/fetch POST request: agents/{botId}/invoke
{
    "name": "tab/fetch",
    "value: {
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
        },
        "context": {
            "theme": "default"
            }
    },
    "conversation": {
        "id": "{generated_conversation_id}"
    },
    "imdisplayname": "{user_display_name}"
}
```

<span data-ttu-id="14a5f-142">**`tab/fetch` ответ**</span><span class="sxs-lookup"><span data-stu-id="14a5f-142">**`tab/fetch` response**</span></span>

```json
// tab/fetch **continue** POST response:
{
    "tab": {
        "type": "continue",
        "value": {
            "cards": [
                {
                    "card": adaptiveCard1,
                },
                {
                    "card": adaptiveCard2,
                }
                {
                    "card": adaptiveCard3
                }  
            ]
        },
    },
    "responseType": "tab"
}
```

### <a name="handle-submits-from-adaptive-card"></a><span data-ttu-id="14a5f-143">Обработка отправки с адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="14a5f-143">Handle submits from Adaptive Card</span></span>

<span data-ttu-id="14a5f-144">После отрисовки адаптивной карты на вкладке она должна быть способна реагировать на взаимодействие пользователей.</span><span class="sxs-lookup"><span data-stu-id="14a5f-144">After an Adaptive Card is rendered in the tab, it must be able to respond to user interactions.</span></span> <span data-ttu-id="14a5f-145">Этот ответ обрабатывается запросом `tab/submit` на вызов.</span><span class="sxs-lookup"><span data-stu-id="14a5f-145">This response is handled by the `tab/submit` invoke request.</span></span>

<span data-ttu-id="14a5f-146">Когда пользователь выбирает кнопку на вкладке Адаптивная карта, запрос запускается в бот с соответствующими данными через функцию `tab/submit` `Action.Submit` Адаптивная карта.</span><span class="sxs-lookup"><span data-stu-id="14a5f-146">When a user selects a button on the Adaptive Card tab, the `tab/submit` request is triggered to your bot with the corresponding data through the `Action.Submit` function of Adaptive Card.</span></span> <span data-ttu-id="14a5f-147">Данные адаптивной карты доступны через свойство данных `tab/submit` запроса.</span><span class="sxs-lookup"><span data-stu-id="14a5f-147">The Adaptive Card data is available through the data property of the `tab/submit` request.</span></span> <span data-ttu-id="14a5f-148">Вы получаете один из следующих ответов на ваш запрос:</span><span class="sxs-lookup"><span data-stu-id="14a5f-148">You receive either of the following responses to your request:</span></span>

* <span data-ttu-id="14a5f-149">Ответ кода состояния `200` HTTP без тела.</span><span class="sxs-lookup"><span data-stu-id="14a5f-149">An HTTP status code `200` response with no body.</span></span> <span data-ttu-id="14a5f-150">Пустые 200 ответов не приводит к действию клиента.</span><span class="sxs-lookup"><span data-stu-id="14a5f-150">An empty 200 response results in no action taken by the client.</span></span>
* <span data-ttu-id="14a5f-151">Стандартная `200` **вкладка продолжает отклик,** как объясняется в [извлечении адаптивной карты.](#fetch-adaptive-card-to-render-to-a-tab)</span><span class="sxs-lookup"><span data-stu-id="14a5f-151">The standard `200` tab **continue** response, as explained in [fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab).</span></span> <span data-ttu-id="14a5f-152">Ответ на **вкладку** продолжает вызывать клиента, чтобы обновить отрисовку вкладки Адаптивная карта с адаптивными картами, предоставляемыми в массиве карт продолжить **ответ.**</span><span class="sxs-lookup"><span data-stu-id="14a5f-152">A tab **continue** response triggers the client to update the rendered Adaptive Card tab with the Adaptive Cards provided in the cards array of the **continue** response.</span></span>

<span data-ttu-id="14a5f-153">В следующем коде приводится пример `tab/submit` запроса и ответа:</span><span class="sxs-lookup"><span data-stu-id="14a5f-153">The following code provides examples of `tab/submit` request and response:</span></span>

<span data-ttu-id="14a5f-154">**`tab/submit` запрос**</span><span class="sxs-lookup"><span data-stu-id="14a5f-154">**`tab/submit` request**</span></span>

```json
// tab/submit POST request: agents/{botId}/invoke:
{
    "name": "tab/submit",
    "value": {
        "data": {
            "type": "tab/submit",
            //...<data properties>
            },
        "context": {
            "theme": "default"
            },
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
            },
        },
    "conversation": {
           "id": "{generated_conversation_id}" 
        },
    "imdisplayname": "{user_display_name}"
}
```

<span data-ttu-id="14a5f-155">**`tab/submit` ответ**</span><span class="sxs-lookup"><span data-stu-id="14a5f-155">**`tab/submit` response**</span></span>

```json
//tab/fetch **continue** POST response:
{
    "tab": {
        "type": "continue",
        "value": {
            "cards": [
              {
                "card": adaptiveCard1,
                },
              {
                "card": adaptiveCard2,
                } 
            ]
        },
    },
    "responseType": "tab"
}
```

## <a name="understand-task-module-workflow"></a><span data-ttu-id="14a5f-156">Понимание рабочего процесса модуля задач</span><span class="sxs-lookup"><span data-stu-id="14a5f-156">Understand task module workflow</span></span>

<span data-ttu-id="14a5f-157">Модуль задач также использует адаптивную карту для вызова `task/fetch` и `task/submit` запросов и ответов.</span><span class="sxs-lookup"><span data-stu-id="14a5f-157">The task module also uses Adaptive Card to invoke `task/fetch` and `task/submit` requests and responses.</span></span> <span data-ttu-id="14a5f-158">Дополнительные сведения см. [в дополнительных сведениях об](../../task-modules-and-cards/task-modules/task-modules-bots.md)использовании модулей задач в Microsoft Teams ботах.</span><span class="sxs-lookup"><span data-stu-id="14a5f-158">For more information, see [using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="14a5f-159">С введением вкладки Adaptive Card меняется реагировать на запрос `task/submit` бота.</span><span class="sxs-lookup"><span data-stu-id="14a5f-159">With the introduction of Adaptive Card tab, there is a change in how the bot responds to a `task/submit` request.</span></span> <span data-ttu-id="14a5f-160">Если вы используете вкладку Адаптивная карта, бот отвечает на запрос вызова со стандартной вкладкой продолжить ответ и закрывает `task/submit` модуль задач. </span><span class="sxs-lookup"><span data-stu-id="14a5f-160">If you are using an Adaptive Card tab, the bot responds to the `task/submit` invoke request with the standard tab **continue** response, and closes the task module.</span></span> <span data-ttu-id="14a5f-161">Вкладка Адаптивная карта обновляется путем отрисовки нового списка карт, предоставленных на вкладке **продолжить** ответ.</span><span class="sxs-lookup"><span data-stu-id="14a5f-161">The Adaptive Card tab is updated by rendering the new list of cards provided in the tab **continue** response body.</span></span>

### <a name="invoke-taskfetch"></a><span data-ttu-id="14a5f-162">Вызов `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="14a5f-162">Invoke `task/fetch`</span></span>

<span data-ttu-id="14a5f-163">В следующем коде приводится пример `task/fetch` запроса и ответа:</span><span class="sxs-lookup"><span data-stu-id="14a5f-163">The following code provides examples of `task/fetch` request and response:</span></span>

<span data-ttu-id="14a5f-164">**`task/fetch` запрос**</span><span class="sxs-lookup"><span data-stu-id="14a5f-164">**`task/fetch` request**</span></span>
```json
// task/fetch POST request: agents/{botId}/invoke
{
    "name": "task/fetch",
    "value": {
        "data": {
            "type": "task/fetch"
        },
        "context": {
            "theme": "default",
        },
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
        }
    },
    "imdisplayname": "{user_display_name}",
    "conversation": {
        "id": "{generated_conversation_id}"
    } 
}
```

<span data-ttu-id="14a5f-165">**`task/fetch` ответ**</span><span class="sxs-lookup"><span data-stu-id="14a5f-165">**`task/fetch` response**</span></span>

```json
// task/fetch POST response: agents/{botId}/invoke
{
    "task": {
        "value": {
            "title": "Ninja Cat",
            "height": "small",
            "width": "small",
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": adaptiveCard,
            }
        },
    "type": "continue"
    },
    "responseType": "task"
}
```

### <a name="invoke-tasksubmit"></a><span data-ttu-id="14a5f-166">Вызов `task/submit`</span><span class="sxs-lookup"><span data-stu-id="14a5f-166">Invoke `task/submit`</span></span>

<span data-ttu-id="14a5f-167">В следующем коде приводится пример `task/submit` запроса и ответа:</span><span class="sxs-lookup"><span data-stu-id="14a5f-167">The following code provides examples of `task/submit` request and response:</span></span>

<span data-ttu-id="14a5f-168">**`task/submit` запрос**</span><span class="sxs-lookup"><span data-stu-id="14a5f-168">**`task/submit` request**</span></span>

```json
// task/submit POST request: agent/{botId}/invoke:
{
    "name": "task/submit",
    "value": {
        "data": {serialized_data_object},
        "context": {
            "theme": "default"
        },
    "tabContext": {
        "tabEntityId": "{tab_entity_id}"
        },
    },
    "conversation": {
        "id": "{generated_conversation_id}"
    },
    "imdisplayname": "{user_display_name}",
}
```

<span data-ttu-id="14a5f-169">**`task/submit` Тип ответа вкладки**</span><span class="sxs-lookup"><span data-stu-id="14a5f-169">**`task/submit` tab response type**</span></span>

```json
// tab/fetch **continue** POST response: 
{
    "task":{
        "value": {
            "tab": {
                "type": "continue",
                "value": {
                    "cards": [
                        {
                            "card": adaptiveCard1
                        },
                        {
                            "card": adaptiveCard2
                        }
                    ]
                }
            }
        },
        "type": "continue"
    },
    "responseType": "task"
}
```

## <a name="authentication"></a><span data-ttu-id="14a5f-170">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="14a5f-170">Authentication</span></span>

<span data-ttu-id="14a5f-171">В предыдущих разделах этой статьи вы видели, что большинство парадигм разработки можно расширить из запросов и ответов модулей задач в запросы и ответы на вкладку.</span><span class="sxs-lookup"><span data-stu-id="14a5f-171">In the previous sections of this article, you have seen that most of the development paradigms can be extended from the task module requests and responses into tab requests and responses.</span></span> <span data-ttu-id="14a5f-172">При обработке проверки подлинности рабочий процесс вкладки Adaptive Card следует шаблону проверки подлинности для расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="14a5f-172">When it comes to handling authentication, the workflow for Adaptive Card tab follows the authentication pattern for messaging extensions.</span></span> <span data-ttu-id="14a5f-173">Дополнительные сведения см. в [добавлении проверки подлинности.](../../messaging-extensions/how-to/add-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="14a5f-173">For more information, see [add authentication](../../messaging-extensions/how-to/add-authentication.md).</span></span>

<span data-ttu-id="14a5f-174">`tab/fetch`запросы могут иметь либо **продолжение,** либо **ответ auth.**</span><span class="sxs-lookup"><span data-stu-id="14a5f-174">`tab/fetch` requests can have either a **continue** or an **auth** response.</span></span> <span data-ttu-id="14a5f-175">Когда запрос запускается и получает ответ auth вкладки, страница входного знака `tab/fetch` отображается пользователю. </span><span class="sxs-lookup"><span data-stu-id="14a5f-175">When a `tab/fetch` request is triggered and receives a tab **auth** response, the sign-in page is shown to the user.</span></span>

<span data-ttu-id="14a5f-176">**Для получения кода проверки подлинности с помощью `tab/fetch` вызова**</span><span class="sxs-lookup"><span data-stu-id="14a5f-176">**To get an authentication code through `tab/fetch` invoke**</span></span>

1. <span data-ttu-id="14a5f-177">Откройте приложение.</span><span class="sxs-lookup"><span data-stu-id="14a5f-177">Open your app.</span></span> <span data-ttu-id="14a5f-178">Появится знак на странице.</span><span class="sxs-lookup"><span data-stu-id="14a5f-178">The sign in page appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="14a5f-179">Логотип приложения предоставляется через `icon` свойство, определенное в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="14a5f-179">The app logo is provided through the `icon` property defined in the app manifest.</span></span> <span data-ttu-id="14a5f-180">Заголовок, появляющийся после определения логотипа в `title` свойстве, возвращаемом в теле ответа **auth** вкладки.</span><span class="sxs-lookup"><span data-stu-id="14a5f-180">The title appearing after the logo is defined in the `title` property returned in the tab **auth** response body.</span></span>

1. <span data-ttu-id="14a5f-181">Щелкните ссылку **Вход**.</span><span class="sxs-lookup"><span data-stu-id="14a5f-181">Select **Sign in**.</span></span> <span data-ttu-id="14a5f-182">Вы перенаправлены на URL-адрес проверки подлинности, предоставленный в свойстве органа `value` ответов **auth.**</span><span class="sxs-lookup"><span data-stu-id="14a5f-182">You are redirected to the authentication URL provided in the `value` property of the **auth** response body.</span></span>
1. <span data-ttu-id="14a5f-183">Открывается всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="14a5f-183">A pop-up window appears.</span></span> <span data-ttu-id="14a5f-184">В этом всплывающее окно размещена веб-страница с помощью URL-адреса проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="14a5f-184">This pop-up window hosts your web page using the authentication URL.</span></span>
1. <span data-ttu-id="14a5f-185">После регистрации закрой окно.</span><span class="sxs-lookup"><span data-stu-id="14a5f-185">After you sign in, close the window.</span></span> <span data-ttu-id="14a5f-186">Код **проверки подлинности** отправляется Teams клиенту.</span><span class="sxs-lookup"><span data-stu-id="14a5f-186">An **authentication code** is sent to the Teams client.</span></span>
1. <span data-ttu-id="14a5f-187">Затем Teams переопроверяет запрос в службу, которая включает код проверки подлинности, предоставляемый на вашей `tab/fetch` веб-странице.</span><span class="sxs-lookup"><span data-stu-id="14a5f-187">The Teams client then reissues the `tab/fetch` request to your service, which includes the authentication code provided by your hosted web page.</span></span>

### <a name="tabfetch-authentication-data-flow"></a><span data-ttu-id="14a5f-188">`tab/fetch` Поток данных проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="14a5f-188">`tab/fetch` authentication data flow</span></span>

<span data-ttu-id="14a5f-189">На следующем изображении представлен обзор работы потока данных проверки подлинности для `tab/fetch` вызова.</span><span class="sxs-lookup"><span data-stu-id="14a5f-189">The following image provides an overview of how the authentication data flow works for a `tab/fetch` invoke.</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Пример потока auth вкладки адаптивной карты." border="false":::

<span data-ttu-id="14a5f-191">**`tab/fetch` ответ auth**</span><span class="sxs-lookup"><span data-stu-id="14a5f-191">**`tab/fetch` auth response**</span></span>

<span data-ttu-id="14a5f-192">В следующем коде приводится пример `tab/fetch` ответа auth:</span><span class="sxs-lookup"><span data-stu-id="14a5f-192">The following code provides an example of `tab/fetch` auth response:</span></span>

```json
// tab/auth POST response (openURL)
{
    "tab": {
        "type": "auth",
        "suggestedActions":{
            "actions":[
                {
                    "type": "openUrl",
                    "value": "https://example.com/auth",
                    "title": "Sign in to this app"
                }
            ]
        }
    }
}
```

### <a name="example"></a><span data-ttu-id="14a5f-193">Пример</span><span class="sxs-lookup"><span data-stu-id="14a5f-193">Example</span></span>

<span data-ttu-id="14a5f-194">В следующем коде показан пример повторного запроса:</span><span class="sxs-lookup"><span data-stu-id="14a5f-194">The following code shows a reissued request example:</span></span>

```json
{
    "name": "tab/fetch",
    "type": "invoke",
    "timestamp": "2021-01-15T00:10:12.253Z",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "{id}",
        "name": "John Smith",
        "aadObjectId": "00000000-0000-0000-0000-000000000000"
    },
    "conversation": {
        "tenantId": "{tenantId}",
        "id": "tab:{guid}"
    },
    "recipients": {
        "id": "28:00000000-0000-0000-0000-000000000000",
        "name": "ContosoApp"
    },
    "entities": [
        {
            "locale": "en-us",
            "country": "US",
            "platform": "Windows",
            "timezone": "America/Los_Angeles",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "tenant": { "id": "00000000-0000-0000-0000-000000000000" },
        "source": { "name": "message" }
    },
    "value": {
        "tabContext": { "tabEntityId": "homeTab" },
        "state": "0.43195668034524815"
    },
    "locale": "en-US",
    "localTimeZone": "America/Los_Angeles"
}
```

## <a name="see-also"></a><span data-ttu-id="14a5f-195">См. также</span><span class="sxs-lookup"><span data-stu-id="14a5f-195">See also</span></span>

* [<span data-ttu-id="14a5f-196">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="14a5f-196">Adaptive Card</span></span>](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [<span data-ttu-id="14a5f-197">Teams вкладки</span><span class="sxs-lookup"><span data-stu-id="14a5f-197">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="14a5f-198">Создание личной вкладки</span><span class="sxs-lookup"><span data-stu-id="14a5f-198">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="14a5f-199">Создание вкладки канала или группы</span><span class="sxs-lookup"><span data-stu-id="14a5f-199">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="14a5f-200">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="14a5f-200">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a><span data-ttu-id="14a5f-201">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="14a5f-201">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="14a5f-202">Предварительный просмотр для ссылки "Вкладки" и представление стадий</span><span class="sxs-lookup"><span data-stu-id="14a5f-202">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)