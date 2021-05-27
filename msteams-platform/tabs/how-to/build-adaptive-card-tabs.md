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
# <a name="build-tabs-with-adaptive-cards"></a>Создание вкладок с помощью адаптивных карт

> [!IMPORTANT]
> * Эта функция находится в [общедоступных Developer Preview](~/resources/dev-preview/developer-preview-intro.md) поддерживается в настольных компьютерах и мобильных устройствах. Поддержка в веб-браузере скоро.
> * Вкладки с адаптивными картами в настоящее время поддерживаются только в качестве личных приложений.

Используйте адаптивные карты для создания вкладок с легкостью. Вы можете создавать вкладки с готовыми блоками Lego пользовательского интерфейса, которые выглядят и чувствуют себя родными на рабочем столе, в Интернете и на мобильных устройствах. Создание вкладок с адаптивными картами централизует все возможности Teams приложений вокруг спинки бота и переднего входа адаптивной карты, таким образом устраняя необходимость в другой задней части для бота и вкладок. Это значительно снижает расходы на сервер и обслуживание вашего Teams приложения. В этой статье вы сможете понять изменения, необходимые для манифеста приложения, как запрашивает действия и отправляет сведения на вкладке с адаптивными картами, а также влияние на рабочий процесс модуля задач. 

На следующем изображении показаны вкладки сборки с адаптивными картами в настольных и мобильных устройствах: пример адаптивной карты, отрисовки :::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="на вкладке." border="false":::

## <a name="prerequisites"></a>Необходимые компоненты

Прежде чем приступить к созданию вкладок с помощью адаптивных карт, необходимо:

* Ознакомьтесь с разработкой [ботов,](../../bots/what-are-bots.md) [адаптивными](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)картами и модулями задач [в](../../task-modules-and-cards/task-modules/task-modules-bots.md) Teams.
* У вас есть бот, работающий в Teams для разработки.
* Будьте в [общедоступных Developer Preview](~/resources/dev-preview/developer-preview-intro.md).

## <a name="changes-to-app-manifest"></a>Изменения манифеста приложений

Личные приложения, которые отрисовка вкладок должны включать `staticTabs` массив в манифест приложения. Адаптивная вкладка карты отрисовка, когда `contentBotId` свойство предоставлено в `staticTab` определении. Статические определения вкладок должны содержать либо вкладку адаптивной карты, либо таблицу, указывав типичную хозяйную вкладку `contentBotId` `contentUrl` веб-контента.

> [!NOTE]
> Свойство `contentBotId` в настоящее время доступно в манифесте версии 1.9 или более поздней версии. 

`contentBotId`Предобередить свойство с помощью `botId` вкладки адаптивной карты. Настроенный для вкладки адаптивной карты отправляется в параметре каждого запроса на вызов и может использоваться для дифференциалов различных вкладок адаптивной карты, которые используются одним и тем же `entityId` `tabContext` ботом. Дополнительные сведения о других полях определения статических вкладок см. в [схеме манифеста.](../../resources/schema/manifest-schema.md#statictabs)

Ниже приводится пример манифеста вкладки адаптивной карты:

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

## <a name="invoke-activities"></a>Вызов действий

Связь между вкладкой адаптивной карты и ботом делается с помощью `invoke` действий. Каждое `invoke` действие имеет соответствующее *имя.* Используйте имя каждого действия, чтобы различать каждый запрос. `tab/fetch` и `tab/submit` являются действиями, охватываемых в этом разделе.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Извлечение адаптивной карты для отрисовки на вкладке

`tab/fetch` это первый запрос на вызов, который ваш бот получает, когда пользователь открывает вкладки адаптивной карты. Когда ваш бот получает запрос, он будет  отправлять вкладку продолжить ответ или ответ **auth вкладки.**
Продолжение **ответа** включает массив для **карт,** который отрисовывется вертикально на вкладку в порядке массива.

> [!NOTE]
> Ответ **auth** подробно объясняется в разделе проверка [подлинности.](#authentication)

Следующие фрагменты кода являются примерами запросов `tab/fetch` и ответов:

**`tab/fetch` запрос**

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

**`tab/fetch` ответ**

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

### <a name="handle-submits-from-adaptive-card"></a>Обработка отправки с адаптивной карты

После отрисовки адаптивной карты на вкладке она должна быть способна реагировать на взаимодействие пользователей. Этот ответ обрабатывается запросом `tab/submit` на вызов.

Когда пользователь выбирает кнопку на вкладке Адаптивная карта, запрос запускается к боту с соответствующими данными с помощью функции `tab/submit` *Action.Submit* адаптивной карты. Данные адаптивной карты доступны через свойство данных `tab/submit` запроса. Вы получите любой из следующих ответов на ваш запрос:

* Ответ кода http `200` status без тела. Пустой 200 ответ не приведет к действию клиента.
* Стандартная `200` **вкладка продолжает отклик,** как поясняется в разделе [Fetch Adaptive Card.](#fetch-adaptive-card-to-render-to-a-tab) Ответ на **вкладку** продолжает вызывать у клиента обновление отрисовки вкладки адаптивной карты с помощью адаптивных карт, предоставляемых в массиве карт с **продолжением ответа.**

Следующие фрагменты кода являются примерами запросов `tab/submit` и ответов:

**`tab/submit` запрос**

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

**`tab/submit` ответ**

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

## <a name="understand-task-module-workflow"></a>Понимание рабочего процесса модуля задач

Модуль задач также использует адаптивную карту для вызова `task/fetch` и `task/submit` запросов и ответов. Дополнительные сведения см. в дополнительных сведениях об использовании модулей задач [в Microsoft Teams ботах.](../../task-modules-and-cards/task-modules/task-modules-bots.md)

Однако с введением вкладки адаптивной карты меняется реагировать на запрос `task/submit` бота. Если вы используете вкладку Адаптивная карта, бот отвечает на запрос вызова со стандартной вкладкой продолжить ответ и закрывает `task/submit` модуль задач.  Вкладка адаптивной карты обновляется путем отрисовки нового списка карт, предоставленных на вкладке **продолжить** ответ.

### <a name="invoke-taskfetch"></a>Вызов `task/fetch`

Следующие фрагменты кода являются примерами запросов `task/fetch` и ответов:

**`task/fetch` запрос**
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

**`task/fetch` ответ**

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

### <a name="invoke-tasksubmit"></a>Вызов `task/submit`

Следующие фрагменты кода являются примерами запросов `task/submit` и ответов:

**`task/submit` запрос**

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

**`task/submit` Тип ответа вкладки**

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

## <a name="authentication"></a>Проверка подлинности

В предыдущих разделах этой статьи вы видели, что большинство парадигм разработки можно экстраполировать из запросов и ответов модулей задач в запросы и ответы на вкладки. Однако при обработке проверки подлинности рабочий процесс для вкладки адаптивной карты следует шаблону проверки подлинности для расширений обмена сообщениями. Дополнительные сведения см. в [добавлении проверки подлинности.](../../messaging-extensions/how-to/add-authentication.md) 

В разделе [действия ссылок](#invoke-activities) вам сообщили, что запросы могут иметь либо `tab/fetch` **продолжение,** либо **ответ auth.** Когда запрос запускается и получает ответ auth вкладки, страница входного знака `tab/fetch` отображается пользователю.  

**Для получения кода проверки подлинности с помощью `tab/fetch` вызова**

1. Откройте приложение. Появится знак на странице.

    > [!NOTE]
    > Логотип приложения предоставляется через свойство, определенное в манифесте приложения, и заголовок, появляющийся после определения логотипа в свойстве, возвращаемом на вкладке `icon` `title` **auth** response body.

1. Щелкните ссылку **Вход**. Вы перенаправлены на URL-адрес проверки подлинности, предоставленный в свойстве органа `value` ответов **auth.** 
1. Открывается всплывающее окно. В этом всплывающее окно размещена веб-страница с помощью URL-адреса проверки подлинности.
1. После регистрации закрой окно. Код *проверки подлинности* отправляется Teams клиенту.
1. Затем Teams переопроверяет запрос в службу, которая включает код проверки подлинности, предоставляемый на вашей `tab/fetch` веб-странице. 

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` Поток данных проверки подлинности

На следующем изображении представлен обзор работы потока данных проверки подлинности для `tab/fetch` вызова.

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Пример потока auth вкладки адаптивной карты." border="false":::

**`tab/fetch` ответ auth**

Следующий фрагмент кода является примером ответа `tab/fetch` auth:

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

### <a name="example"></a>Пример

Ниже показан пример повторного запроса:

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

## <a name="see-also"></a>См. также

> [!div class="nextstepaction"]
> [Адаптивная карта](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)

