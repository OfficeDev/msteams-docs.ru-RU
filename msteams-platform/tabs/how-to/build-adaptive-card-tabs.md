---
title: Создание вкладок адаптивной карты
author: KirtiPereira
description: Узнайте о создании вкладок с использованием адаптивных карт с примерами кода, включая действия по ссылке, понимание рабочего процесса модуля задач и проверку подлинности.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: поток данных проверки подлинности персональных приложений адаптивной карты
ms.openlocfilehash: 2747dbe089ee847e7f5465d3a19fa58dbf945be5
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453266"
---
# <a name="build-tabs-with-adaptive-cards"></a>Создание вкладок с использованием адаптивных карточек

> [!IMPORTANT]
>
> * Вкладки с адаптивными картами в настоящее время поддерживаются только в качестве личных приложений.

При разработке вкладки с помощью традиционного метода могут возникнуть такие проблемы:

* Соображения HTML и CSS
* Медленное время загрузки
* Ограничения iFrame
* Обслуживание серверов и затраты

Адаптивные вкладки карты — это новый способ создания вкладок в Teams. Вместо встраив веб-контент в IFrame, вы можете отрисовки адаптивных карт на вкладку. В то время как передняя часть отрисовывана с помощью адаптивных карт, задний задаток будет работать с помощью бота. Бот отвечает за прием запросов и соответствующий ответ с помощью отрисовки адаптивной карты.

Вы можете создавать вкладки с помощью готовых блоков пользовательского интерфейса (пользовательского интерфейса) на рабочем столе, в Интернете и на мобильных устройствах. В этой статье вы сможете понять изменения, необходимые для манифеста приложения. В статье также указывается, как запросы на действия вызываемого вызова и отправка сведений на вкладке с помощью адаптивных карт, а также ее влияние на рабочий процесс модуля задач.

На следующем изображении показаны вкладки сборки с адаптивными картами в настольных и мобильных устройствах:

:::image type="content" source="../../assets/images/adaptive-cards-rendered-in-tabs.png" alt-text="Пример адаптивной карты, отрисовываемой на вкладке." border="false":::

## <a name="prerequisites"></a>Предварительные условия

Прежде чем приступить к созданию вкладок с помощью адаптивных карт, необходимо:

* Ознакомьтесь с [разработкой ботов](../../bots/what-are-bots.md), [адаптивными](https://adaptivecards.io/) картами и модулями задач в Teams.[](../../task-modules-and-cards/task-modules/task-modules-bots.md)
* У вас есть бот, работающий Teams для разработки.

## <a name="changes-to-app-manifest"></a>Изменения манифеста приложений

Личные приложения, которые отрисовка вкладок должны включать массив `staticTabs` в манифест приложения. Вкладки адаптивной карты отрисовываться, когда `contentBotId` свойство предоставлено в определении `staticTab` . Статические определения вкладок `contentBotId``contentUrl`должны содержать либо вкладку Адаптивная карточка, либо типичную хозяйную вкладку веб-контента.

> [!NOTE]
> Свойство `contentBotId` в настоящее время доступно в манифестной версии 1.9 или более поздней версии.

Предобередим `contentBotId` свойство вкладке `botId` Adaptive Card, с которую необходимо связаться. Настроенная `entityId` для вкладки Адаптивная `tabContext` карта отправляется в параметре каждого запроса на вызов и может использоваться для дифференцировать вкладки адаптивной карты, которые используются одним и тем же ботом. Дополнительные сведения о других полях определения статических вкладок см. в [схеме манифеста](../../resources/schema/manifest-schema.md#statictabs).

Ниже приводится пример манифеста вкладки Адаптивная карта:

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

Связь между вкладкой Адаптивная карта и ботом делается с помощью действий `invoke` . Каждое `invoke` действие имеет соответствующее **имя**. Используйте имя каждого действия, чтобы различать каждый запрос. `tab/fetch` и `tab/submit` являются действиями, охватываемых в этом разделе.

> [!NOTE]
>
> * Боты должны отправлять все ответы на [URL-адрес службы](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true). URL-адрес службы получается в составе входящих полезной `activity` нагрузки.
> * Размер полезной нагрузки вызова увеличен до 80kb.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Извлечение адаптивной карты для отрисовки на вкладке

`tab/fetch`это первый запрос на вызов, который ваш бот получает, когда пользователь открывает вкладку Адаптивная карта. Когда ваш бот получает запрос, он отправляет вкладку продолжить ответ или ответ  **auth вкладки**.
Продолжение **ответа** включает массив для **карт**, который отрисовывется вертикально на вкладку в порядке массива.

> [!NOTE]
> Дополнительные сведения о **ответе auth** см. в [сайте проверки подлинности](#authentication).

В следующем коде приводится пример запроса `tab/fetch` и ответа:

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
                },
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

После отрисовки адаптивной карты на вкладке она может реагировать на взаимодействие пользователей. Этот ответ обрабатывается запросом на `tab/submit` вызов.

Когда пользователь выбирает кнопку на вкладке Адаптивная карта, `tab/submit` `Action.Submit` запрос запускается в бот с соответствующими данными через функцию Адаптивная карта. Данные адаптивной карты доступны через свойство данных запроса `tab/submit` . Вы получаете один из следующих ответов на ваш запрос:

* Ответ кода состояния `200` HTTP без тела. Пустые 200 ответов не приводит к действию клиента.
* Стандартная вкладка `200` **продолжает отклик** , как объясняется в [извлечении адаптивной карты](#fetch-adaptive-card-to-render-to-a-tab). Ответ на **вкладку** продолжает вызывать клиента, чтобы обновить отрисовку вкладки Адаптивная карта с адаптивными картами, предоставляемыми в массиве карт продолжить **ответ** .

В следующем коде приводится пример запроса `tab/submit` и ответа:

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

Модуль задач также использует адаптивную карту для вызова `task/fetch` и `task/submit` запросов и ответов. Дополнительные сведения см. в [дополнительных сведениях об использовании модулей задач в Microsoft Teams ботах](../../task-modules-and-cards/task-modules/task-modules-bots.md).

С введением вкладки Адаптивная `task/submit` карта меняется реагировать на запрос бота. Если вы используете вкладку Adaptive Card, `task/submit` бот отвечает на запрос на вызов со стандартной вкладкой продолжить ответ и закрывает  модуль задач. Вкладка Адаптивная карта обновляется путем отрисовки нового списка карт, предоставленных на вкладке **продолжить** ответ.

### <a name="invoke-taskfetch"></a>Вызов `task/fetch`

В следующем коде приводится пример запроса `task/fetch` и ответа:

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

В следующем коде приводится пример запроса `task/submit` и ответа:

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

В предыдущих разделах вы видели, что большинство парадигм разработки можно расширить из запросов и ответов модулей задач в запросы и ответы на вкладки. При обработке проверки подлинности рабочий процесс вкладки Adaptive Card следует шаблону проверки подлинности для расширений обмена сообщениями. Дополнительные сведения см. в [добавлении проверки подлинности](../../messaging-extensions/how-to/add-authentication.md).

`tab/fetch` запросы могут иметь либо продолжение **,** либо **ответ auth** . Когда запрос `tab/fetch` запускается и получает ответ на вкладку **auth** , пользователю отображается вход на страницу.

**Для получения кода проверки подлинности с помощью вызова `tab/fetch`**

1. Откройте приложение. Появится знак на странице.

    > [!NOTE]
    > Логотип приложения предоставляется через свойство `icon` , определенное в манифесте приложения. Заголовок, появляющийся `title` после определения логотипа в свойстве, возвращаемом в теле ответа **auth** вкладки.

1. Щелкните ссылку **Войти**. Вы перенаправляетсяе на URL-адрес проверки подлинности, предоставленный в `value` свойстве органа ответов **auth** .
1. Открывается всплывающее окно. В этом всплывающее окно размещена веб-страница с помощью URL-адреса проверки подлинности.
1. После регистрации закрой окно. Код **проверки подлинности** отправляется Teams клиенту.
1. Затем Teams `tab/fetch` переопроверяет запрос в службу, которая включает код проверки подлинности, предоставляемый на веб-странице.

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` Поток данных проверки подлинности

На следующем изображении представлен обзор работы потока данных проверки подлинности для вызова `tab/fetch` .

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Пример потока auth вкладки адаптивной карты." border="false":::

**`tab/fetch` ответ auth**

В следующем коде приводится пример ответа `tab/fetch` auth:

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

В следующем коде показан пример повторного запроса:

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

## <a name="code-sample"></a>Пример кода

|**Название примера** | **Описание** |**.NET** | **Node.js** |
|----------------|-----------------|--------------|--------------|
| Показать адаптивные карты на вкладке Teams | Microsoft Teams пример кода вкладки, который демонстрирует, как показывать адаптивные карты в Teams. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Вкладки связывают разгрузку и представление сцены](~/tabs/tabs-link-unfurling.md)

## <a name="see-also"></a>См. также

* [Адаптивная карточка](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Teams вкладки](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Отзывы о завершении формы](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
