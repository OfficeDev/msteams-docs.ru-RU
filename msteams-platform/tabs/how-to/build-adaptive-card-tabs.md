---
title: Создание вкладок адаптивной карты
author: KirtiPereira
description: Создание вкладок с помощью адаптивных карт
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: d65fc537b5282c050d891a6a73ff114c630e2c1c
ms.sourcegitcommit: c59d90ae03eae32996db49f162855965b55c52fe
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/26/2021
ms.locfileid: "52668850"
---
# <a name="build-tabs-with-adaptive-cards"></a><span data-ttu-id="67bc5-103">Создание вкладок с использованием адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="67bc5-103">Build tabs with Adaptive Cards</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="67bc5-104">Эта функция находится в [общедоступных Developer Preview](~/resources/dev-preview/developer-preview-intro.md) поддерживается в настольных компьютерах и мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="67bc5-104">This feature is in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) and is supported in desktop and mobile.</span></span> <span data-ttu-id="67bc5-105">Поддержка в веб-браузере скоро.</span><span class="sxs-lookup"><span data-stu-id="67bc5-105">Support in the web browser is coming soon.</span></span>
> * <span data-ttu-id="67bc5-106">Вкладки с адаптивными картами в настоящее время поддерживаются только в качестве личных приложений.</span><span class="sxs-lookup"><span data-stu-id="67bc5-106">Tabs with Adaptive Cards are currently only supported as personal apps.</span></span>

<span data-ttu-id="67bc5-107">Используйте адаптивные карты для создания вкладок с легкостью.</span><span class="sxs-lookup"><span data-stu-id="67bc5-107">Use Adaptive Cards to build tabs with ease.</span></span> <span data-ttu-id="67bc5-108">Вы можете создавать вкладки с готовыми блоками Lego пользовательского интерфейса, которые выглядят и чувствуют себя родными на рабочем столе, в Интернете и на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="67bc5-108">You can build your tabs with ready-made UI Lego-blocks that look and feel native on desktop, web, and mobile.</span></span> <span data-ttu-id="67bc5-109">Создание вкладок с адаптивными картами централизует все возможности Teams приложений вокруг спинки бота и переднего входа адаптивной карты, таким образом устраняя необходимость в другой задней части для бота и вкладок.</span><span class="sxs-lookup"><span data-stu-id="67bc5-109">Building tabs with Adaptive Cards centralizes all Teams app capabilities around a bot backend and Adaptive Card frontend, thus, eliminating the need for a different backend for your bot and tabs.</span></span> <span data-ttu-id="67bc5-110">Это значительно снижает расходы на сервер и обслуживание вашего Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="67bc5-110">This greatly reduces server and maintenance costs of your Teams app.</span></span> <span data-ttu-id="67bc5-111">В этой статье вы сможете понять изменения, необходимые для манифеста приложения, как запрашивает действия и отправляет сведения на вкладке с адаптивными картами, а также влияние на рабочий процесс модуля задач.</span><span class="sxs-lookup"><span data-stu-id="67bc5-111">This article helps you understand the changes required to be made to the app manifest, how the invoke activity requests and sends information in tab with Adaptive Cards, and the impact on the task module workflow.</span></span> 

На следующем изображении показаны вкладки сборки с адаптивными картами в настольных и мобильных устройствах: пример адаптивной карты, отрисовки :::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="на вкладке." border="false":::

## <a name="prerequisites"></a><span data-ttu-id="67bc5-113">Предварительные условия</span><span class="sxs-lookup"><span data-stu-id="67bc5-113">Prerequisites</span></span>

<span data-ttu-id="67bc5-114">Прежде чем приступить к созданию вкладок с помощью адаптивных карт, необходимо:</span><span class="sxs-lookup"><span data-stu-id="67bc5-114">Before you start using Adaptive Cards to build tabs, you must:</span></span>

* <span data-ttu-id="67bc5-115">Ознакомьтесь с разработкой [ботов,](../../bots/what-are-bots.md) [адаптивными](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)картами и модулями задач [в](../../task-modules-and-cards/task-modules/task-modules-bots.md) Teams.</span><span class="sxs-lookup"><span data-stu-id="67bc5-115">Be familiar with, [bot development](../../bots/what-are-bots.md), [Adaptive Cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards), and [Task Modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) in Teams.</span></span>
* <span data-ttu-id="67bc5-116">У вас есть бот, работающий в Teams для разработки.</span><span class="sxs-lookup"><span data-stu-id="67bc5-116">Have a bot running in Teams for your development.</span></span>
* <span data-ttu-id="67bc5-117">Будьте в [общедоступных Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="67bc5-117">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="changes-to-app-manifest"></a><span data-ttu-id="67bc5-118">Изменения манифеста приложений</span><span class="sxs-lookup"><span data-stu-id="67bc5-118">Changes to app manifest</span></span>

<span data-ttu-id="67bc5-119">Личные приложения, которые отрисовка вкладок должны включать `staticTabs` массив в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="67bc5-119">Personal apps that render tabs must include a `staticTabs` array in their app manifest.</span></span> <span data-ttu-id="67bc5-120">Адаптивная вкладка карты отрисовка, когда `contentBotId` свойство предоставлено в `staticTab` определении.</span><span class="sxs-lookup"><span data-stu-id="67bc5-120">Adaptive Card Tab are rendered when the `contentBotId` property is provided in the `staticTab` definition.</span></span> <span data-ttu-id="67bc5-121">Статические определения вкладок должны содержать либо вкладку адаптивной карты, либо таблицу, указывав типичную хозяйную вкладку `contentBotId` `contentUrl` веб-контента.</span><span class="sxs-lookup"><span data-stu-id="67bc5-121">Static tab definitions must contain either a `contentBotId`, specifying an Adaptive Card Tab or a `contentUrl`, specifying a typical hosted web content tab experience.</span></span>

> [!NOTE]
> <span data-ttu-id="67bc5-122">Свойство `contentBotId` в настоящее время доступно в манифесте версии 1.9 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="67bc5-122">The `contentBotId` property is currently available manifest version 1.9 or later.</span></span> 

<span data-ttu-id="67bc5-123">`contentBotId`Предобередить свойство с помощью `botId` вкладки адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="67bc5-123">Provide the `contentBotId` property with the `botId` that the Adaptive Card Tab must communicate with.</span></span> <span data-ttu-id="67bc5-124">Настроенный для вкладки адаптивной карты отправляется в параметре каждого запроса на вызов и может использоваться для дифференциалов различных вкладок адаптивной карты, которые используются одним и тем же `entityId` `tabContext` ботом.</span><span class="sxs-lookup"><span data-stu-id="67bc5-124">The `entityId` configured for the Adaptive Card Tab is sent in the `tabContext` parameter of each invoke request, and can be used to differentiate different Adaptive Card Tabs that are powered by the same bot.</span></span> <span data-ttu-id="67bc5-125">Дополнительные сведения о других полях определения статических вкладок см. в [схеме манифеста.](../../resources/schema/manifest-schema.md#statictabs)</span><span class="sxs-lookup"><span data-stu-id="67bc5-125">For more information about other static tab definition fields, see [manifest schema](../../resources/schema/manifest-schema.md#statictabs).</span></span>

<span data-ttu-id="67bc5-126">Ниже приводится пример манифеста вкладки адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="67bc5-126">Following is a sample Adaptive Card Tab manifest:</span></span>

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

## <a name="invoke-activities"></a><span data-ttu-id="67bc5-127">Вызов действий</span><span class="sxs-lookup"><span data-stu-id="67bc5-127">Invoke activities</span></span>

<span data-ttu-id="67bc5-128">Связь между вкладкой адаптивной карты и ботом делается с помощью `invoke` действий.</span><span class="sxs-lookup"><span data-stu-id="67bc5-128">Communication between your Adaptive Card Tab and your bot is done through `invoke` activities.</span></span> <span data-ttu-id="67bc5-129">Каждое `invoke` действие имеет соответствующее *имя.*</span><span class="sxs-lookup"><span data-stu-id="67bc5-129">Each `invoke` activity has a corresponding *name*.</span></span> <span data-ttu-id="67bc5-130">Используйте имя каждого действия, чтобы различать каждый запрос.</span><span class="sxs-lookup"><span data-stu-id="67bc5-130">Use the name of each activity to differentiate each request.</span></span> <span data-ttu-id="67bc5-131">`tab/fetch` и `tab/submit` являются действиями, охватываемых в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="67bc5-131">`tab/fetch` and `tab/submit` are the activities covered in this section.</span></span>

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a><span data-ttu-id="67bc5-132">Извлечение адаптивной карты для отрисовки на вкладке</span><span class="sxs-lookup"><span data-stu-id="67bc5-132">Fetch Adaptive Card to render to a tab</span></span>

<span data-ttu-id="67bc5-133">`tab/fetch` это первый запрос на вызов, который ваш бот получает, когда пользователь открывает вкладки адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="67bc5-133">`tab/fetch` is the first invoke request that your bot receives when a user opens an Adaptive Card Tabs.</span></span> <span data-ttu-id="67bc5-134">Когда ваш бот получает запрос, он будет  отправлять вкладку продолжить ответ или ответ **auth вкладки.**</span><span class="sxs-lookup"><span data-stu-id="67bc5-134">When your bot receives the request, it will either send a tab **continue** response or a tab **auth** response.</span></span>
<span data-ttu-id="67bc5-135">Продолжение **ответа** включает массив для **карт,** который отрисовывется вертикально на вкладку в порядке массива.</span><span class="sxs-lookup"><span data-stu-id="67bc5-135">The **continue** response includes an array for **cards**, which is rendered vertically to the tab in the order of the array.</span></span>

> [!NOTE]
> <span data-ttu-id="67bc5-136">Ответ **auth** подробно объясняется в разделе проверка [подлинности.](#authentication)</span><span class="sxs-lookup"><span data-stu-id="67bc5-136">The **auth** response is explained in detail in the [authentication](#authentication) section.</span></span>

<span data-ttu-id="67bc5-137">Следующие фрагменты кода являются примерами запросов `tab/fetch` и ответов:</span><span class="sxs-lookup"><span data-stu-id="67bc5-137">The following code snippets are examples of `tab/fetch` request and response:</span></span>

<span data-ttu-id="67bc5-138">**`tab/fetch` запрос**</span><span class="sxs-lookup"><span data-stu-id="67bc5-138">**`tab/fetch` request**</span></span>

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

<span data-ttu-id="67bc5-139">**`tab/fetch` ответ**</span><span class="sxs-lookup"><span data-stu-id="67bc5-139">**`tab/fetch` response**</span></span>

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

### <a name="handle-submits-from-adaptive-card"></a><span data-ttu-id="67bc5-140">Обработка отправки с адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="67bc5-140">Handle submits from Adaptive Card</span></span>

<span data-ttu-id="67bc5-141">После отрисовки адаптивной карты на вкладке она должна быть способна реагировать на взаимодействие пользователей.</span><span class="sxs-lookup"><span data-stu-id="67bc5-141">After an Adaptive Card is rendered in the tab, it must be able to respond to user interactions.</span></span> <span data-ttu-id="67bc5-142">Этот ответ обрабатывается запросом `tab/submit` на вызов.</span><span class="sxs-lookup"><span data-stu-id="67bc5-142">This response is handled by the `tab/submit` invoke request.</span></span>

<span data-ttu-id="67bc5-143">Когда пользователь выбирает кнопку на вкладке Адаптивная карта, запрос запускается к боту с соответствующими данными с помощью функции `tab/submit` *Action.Submit* адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="67bc5-143">When a user selects a button on the Adaptive Card Tab, the `tab/submit` request is triggered to your bot with the corresponding data through the *Action.Submit* function of Adaptive Card.</span></span> <span data-ttu-id="67bc5-144">Данные адаптивной карты доступны через свойство данных `tab/submit` запроса.</span><span class="sxs-lookup"><span data-stu-id="67bc5-144">The Adaptive Card data is available through the data property of the `tab/submit` request.</span></span> <span data-ttu-id="67bc5-145">Вы получите любой из следующих ответов на ваш запрос:</span><span class="sxs-lookup"><span data-stu-id="67bc5-145">You will receive either of the following responses to your request:</span></span>

* <span data-ttu-id="67bc5-146">Ответ кода http `200` status без тела.</span><span class="sxs-lookup"><span data-stu-id="67bc5-146">A http status code `200` response with no body.</span></span> <span data-ttu-id="67bc5-147">Пустой 200 ответ не приведет к действию клиента.</span><span class="sxs-lookup"><span data-stu-id="67bc5-147">An empty 200 response will result in no action taken by the client.</span></span>
* <span data-ttu-id="67bc5-148">Стандартная `200` **вкладка продолжает отклик,** как поясняется в разделе [Fetch Adaptive Card.](#fetch-adaptive-card-to-render-to-a-tab)</span><span class="sxs-lookup"><span data-stu-id="67bc5-148">The standard `200` tab **continue** response, as explained in [Fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab) section.</span></span> <span data-ttu-id="67bc5-149">Ответ на **вкладку** продолжает вызывать у клиента обновление отрисовки вкладки адаптивной карты с помощью адаптивных карт, предоставляемых в массиве карт с **продолжением ответа.**</span><span class="sxs-lookup"><span data-stu-id="67bc5-149">A tab **continue** response triggers the client to update the rendered Adaptive Card Tab with the Adaptive Cards provided in the cards array of the **continue** response.</span></span>

<span data-ttu-id="67bc5-150">Следующие фрагменты кода являются примерами запросов `tab/submit` и ответов:</span><span class="sxs-lookup"><span data-stu-id="67bc5-150">The following code snippets are examples of `tab/submit` request and response:</span></span>

<span data-ttu-id="67bc5-151">**`tab/submit` запрос**</span><span class="sxs-lookup"><span data-stu-id="67bc5-151">**`tab/submit` request**</span></span>

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

<span data-ttu-id="67bc5-152">**`tab/submit` ответ**</span><span class="sxs-lookup"><span data-stu-id="67bc5-152">**`tab/submit` response**</span></span>

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

## <a name="understand-task-module-workflow"></a><span data-ttu-id="67bc5-153">Понимание рабочего процесса модуля задач</span><span class="sxs-lookup"><span data-stu-id="67bc5-153">Understand task module workflow</span></span>

<span data-ttu-id="67bc5-154">Модуль задач также использует адаптивную карту для вызова `task/fetch` и `task/submit` запросов и ответов.</span><span class="sxs-lookup"><span data-stu-id="67bc5-154">The task module also uses Adaptive Card to invoke `task/fetch` and `task/submit` requests and responses.</span></span> <span data-ttu-id="67bc5-155">Дополнительные сведения см. в дополнительных сведениях об использовании модулей задач [в Microsoft Teams ботах.](../../task-modules-and-cards/task-modules/task-modules-bots.md)</span><span class="sxs-lookup"><span data-stu-id="67bc5-155">For more information, see [Using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="67bc5-156">Однако с введением вкладки адаптивной карты меняется реагировать на запрос `task/submit` бота.</span><span class="sxs-lookup"><span data-stu-id="67bc5-156">However, with the introduction of Adaptive Card Tab there is a change in how the bot responds to a `task/submit` request.</span></span> <span data-ttu-id="67bc5-157">Если вы используете вкладку Адаптивная карта, бот отвечает на запрос вызова со стандартной вкладкой продолжить ответ и закрывает `task/submit` модуль задач. </span><span class="sxs-lookup"><span data-stu-id="67bc5-157">If you are using an Adaptive Card Tab, the bot responds to the `task/submit` invoke request with the standard tab **continue** response, and closes the task module.</span></span> <span data-ttu-id="67bc5-158">Вкладка адаптивной карты обновляется путем отрисовки нового списка карт, предоставленных на вкладке **продолжить** ответ.</span><span class="sxs-lookup"><span data-stu-id="67bc5-158">The Adaptive Card Tab is updated by rendering the new list of cards provided in the tab **continue** response body.</span></span>

### <a name="invoke-taskfetch"></a><span data-ttu-id="67bc5-159">Вызов `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="67bc5-159">Invoke `task/fetch`</span></span>

<span data-ttu-id="67bc5-160">Следующие фрагменты кода являются примерами запросов `task/fetch` и ответов:</span><span class="sxs-lookup"><span data-stu-id="67bc5-160">The following code snippets are examples of `task/fetch` request and response:</span></span>

<span data-ttu-id="67bc5-161">**`task/fetch` запрос**</span><span class="sxs-lookup"><span data-stu-id="67bc5-161">**`task/fetch` request**</span></span>
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

<span data-ttu-id="67bc5-162">**`task/fetch` ответ**</span><span class="sxs-lookup"><span data-stu-id="67bc5-162">**`task/fetch` response**</span></span>

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

### <a name="invoke-tasksubmit"></a><span data-ttu-id="67bc5-163">Вызов `task/submit`</span><span class="sxs-lookup"><span data-stu-id="67bc5-163">Invoke `task/submit`</span></span>

<span data-ttu-id="67bc5-164">Следующие фрагменты кода являются примерами запросов `task/submit` и ответов:</span><span class="sxs-lookup"><span data-stu-id="67bc5-164">The following code snippets are examples of `task/submit` request and response:</span></span>

<span data-ttu-id="67bc5-165">**`task/submit` запрос**</span><span class="sxs-lookup"><span data-stu-id="67bc5-165">**`task/submit` request**</span></span>

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

<span data-ttu-id="67bc5-166">**`task/submit` Тип ответа вкладки**</span><span class="sxs-lookup"><span data-stu-id="67bc5-166">**`task/submit` tab response type**</span></span>

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

## <a name="authentication"></a><span data-ttu-id="67bc5-167">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="67bc5-167">Authentication</span></span>

<span data-ttu-id="67bc5-168">В предыдущих разделах этой статьи вы видели, что большинство парадигм разработки можно экстраполировать из запросов и ответов модулей задач в запросы и ответы на вкладки.</span><span class="sxs-lookup"><span data-stu-id="67bc5-168">In the previous sections of this article, you have seen that most of the development paradigms could be extrapolated from the task module requests and responses into tab requests and responses.</span></span> <span data-ttu-id="67bc5-169">Однако при обработке проверки подлинности рабочий процесс для вкладки адаптивной карты следует шаблону проверки подлинности для расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="67bc5-169">However, when it comes to handling authentication, the workflow for Adaptive Card Tab follows the authentication pattern for messaging extensions.</span></span> <span data-ttu-id="67bc5-170">Дополнительные сведения см. в [добавлении проверки подлинности.](../../messaging-extensions/how-to/add-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="67bc5-170">For more information, see [add authentication](../../messaging-extensions/how-to/add-authentication.md).</span></span> 

<span data-ttu-id="67bc5-171">В разделе [действия ссылок](#invoke-activities) вам сообщили, что запросы могут иметь либо `tab/fetch` **продолжение,** либо **ответ auth.**</span><span class="sxs-lookup"><span data-stu-id="67bc5-171">In the [invoke activities](#invoke-activities) section, you were informed that `tab/fetch` requests can have either a **continue** or an **auth** response.</span></span> <span data-ttu-id="67bc5-172">Когда запрос запускается и получает ответ auth вкладки, страница входного знака `tab/fetch` отображается пользователю. </span><span class="sxs-lookup"><span data-stu-id="67bc5-172">When a `tab/fetch` request is triggered and receives a tab **auth** response, the sign-in page is shown to the user.</span></span> 

<span data-ttu-id="67bc5-173">**Для получения кода проверки подлинности с помощью `tab/fetch` вызова**</span><span class="sxs-lookup"><span data-stu-id="67bc5-173">**To get an authentication code through `tab/fetch` invoke**</span></span>

1. <span data-ttu-id="67bc5-174">Откройте приложение.</span><span class="sxs-lookup"><span data-stu-id="67bc5-174">Open your app.</span></span> <span data-ttu-id="67bc5-175">Появится знак на странице.</span><span class="sxs-lookup"><span data-stu-id="67bc5-175">The sign in page appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="67bc5-176">Логотип приложения предоставляется через свойство, определенное в манифесте приложения, и заголовок, появляющийся после определения логотипа в свойстве, возвращаемом на вкладке `icon` `title` **auth** response body.</span><span class="sxs-lookup"><span data-stu-id="67bc5-176">The app logo is provided through the `icon` property defined in the app manifest, and the title appearing after the logo is defined in the `title` property returned in the tab **auth** response body.</span></span>

1. <span data-ttu-id="67bc5-177">Щелкните ссылку **Вход**.</span><span class="sxs-lookup"><span data-stu-id="67bc5-177">Select **Sign in**.</span></span> <span data-ttu-id="67bc5-178">Вы перенаправлены на URL-адрес проверки подлинности, предоставленный в свойстве органа `value` ответов **auth.**</span><span class="sxs-lookup"><span data-stu-id="67bc5-178">You are redirected to the authentication URL provided in the `value` property of the **auth** response body.</span></span> 
1. <span data-ttu-id="67bc5-179">Открывается всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="67bc5-179">A pop-up window appears.</span></span> <span data-ttu-id="67bc5-180">В этом всплывающее окно размещена веб-страница с помощью URL-адреса проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="67bc5-180">This pop-up window hosts your web page using the authentication URL.</span></span>
1. <span data-ttu-id="67bc5-181">После регистрации закрой окно.</span><span class="sxs-lookup"><span data-stu-id="67bc5-181">After you sign in, close the window.</span></span> <span data-ttu-id="67bc5-182">Код *проверки подлинности* отправляется Teams клиенту.</span><span class="sxs-lookup"><span data-stu-id="67bc5-182">An *authentication code* is sent to the Teams client.</span></span>
1. <span data-ttu-id="67bc5-183">Затем Teams переопроверяет запрос в службу, которая включает код проверки подлинности, предоставляемый на вашей `tab/fetch` веб-странице.</span><span class="sxs-lookup"><span data-stu-id="67bc5-183">The Teams client then reissues the `tab/fetch` request to your service, which includes the authentication code provided by your hosted web page.</span></span> 

### <a name="tabfetch-authentication-data-flow"></a><span data-ttu-id="67bc5-184">`tab/fetch` Поток данных проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="67bc5-184">`tab/fetch` authentication data flow</span></span>

<span data-ttu-id="67bc5-185">На следующем изображении представлен обзор работы потока данных проверки подлинности для `tab/fetch` вызова.</span><span class="sxs-lookup"><span data-stu-id="67bc5-185">The following image provides an overview of how the authentication data flow works for a `tab/fetch` invoke.</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Пример потока auth вкладки адаптивной карты." border="false":::

<span data-ttu-id="67bc5-187">**`tab/fetch` ответ auth**</span><span class="sxs-lookup"><span data-stu-id="67bc5-187">**`tab/fetch` auth response**</span></span>

<span data-ttu-id="67bc5-188">Следующий фрагмент кода является примером ответа `tab/fetch` auth:</span><span class="sxs-lookup"><span data-stu-id="67bc5-188">The following code snippet is an example of `tab/fetch` auth response:</span></span>

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

### <a name="example"></a><span data-ttu-id="67bc5-189">Пример</span><span class="sxs-lookup"><span data-stu-id="67bc5-189">Example</span></span>

<span data-ttu-id="67bc5-190">Ниже показан пример повторного запроса:</span><span class="sxs-lookup"><span data-stu-id="67bc5-190">The following shows a reissued request example:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="67bc5-191">См. также</span><span class="sxs-lookup"><span data-stu-id="67bc5-191">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="67bc5-192">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="67bc5-192">Adaptive Card</span></span>](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)

