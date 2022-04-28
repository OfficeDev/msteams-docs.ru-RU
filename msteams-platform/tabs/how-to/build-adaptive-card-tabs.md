---
title: Создание вкладок адаптивных карточек
author: KirtiPereira
description: Сведения о создании вкладок с помощью адаптивных карточек с примерами кода, включая вызов действий, понимание рабочего процесса модуля задач и проверку подлинности.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: Поток данных для проверки подлинности личного приложения адаптивной карточки
ms.openlocfilehash: 95507373671f9044bec788e981f66931b4588705
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104527"
---
# <a name="build-tabs-with-adaptive-cards"></a>Создание вкладок с использованием адаптивных карточек

> [!IMPORTANT]
>
> * Вкладки с адаптивными карточками в настоящее время поддерживаются только как личные приложения.

При разработке вкладки с помощью традиционного метода могут возникнуть следующие проблемы:

* Рекомендации по HTML и CSS
* Медленное время загрузки
* Ограничения iFrame
* Обслуживание и затраты на сервер

Адаптивные вкладки карточек — это новый способ создания вкладок в Teams. Вместо внедрения веб-содержимого в IFrame адаптивные карточки можно преобразовать на вкладку. При отрисовке внешнего интерфейса с помощью адаптивных карточек серверная часть поддерживается ботом. Бот отвечает за принятие запросов и соответствующий ответ с помощью отрисовки адаптивной карточки.

Вы можете создавать вкладки с помощью готовых стандартных блоков пользовательского интерфейса на настольном компьютере, в Интернете и на мобильных устройствах. Эта статья поможет вам понять, какие изменения необходимо внести в манифест приложения. В этой статье также описывается, как действие вызова запрашивает и отправляет сведения на вкладке с адаптивными карточками и влияет на рабочий процесс модуля задач.

На следующем рисунке показаны вкладки сборки с адаптивными карточками на настольном компьютере и мобильном устройстве:

:::image type="content" source="../../assets/images/adaptive-cards-rendered-in-tabs.png" alt-text="Пример адаптивной карточки, отображаемой на вкладке." border="false":::

## <a name="prerequisites"></a>Предварительные требования

Прежде чем приступить к созданию вкладок с помощью адаптивных карточек, необходимо:

* Ознакомьтесь с [разработкой ботов](../../bots/what-are-bots.md), [адаптивными](https://adaptivecards.io/) карточками и модулями [задач в Teams](../../task-modules-and-cards/task-modules/task-modules-bots.md).
* У вас есть бот, работающий Teams для разработки.

## <a name="changes-to-app-manifest"></a>Изменения манифеста приложения

Личные приложения, которые отображают вкладки, должны содержать массив `staticTabs` в манифесте приложения. Адаптивные вкладки карточек отображаются, когда `contentBotId` свойство указано в определении `staticTab` . Статические определения вкладок `contentBotId`должны содержать либо вкладку адаптивной `contentUrl`карточки, либо типичная вкладка размещенного веб-содержимого.

> [!NOTE]
> Это `contentBotId` свойство в настоящее время доступно в манифесте версии 1.9 или более поздней.

Укажите свойство `contentBotId` , с `botId` помощью которого должна взаимодействовать вкладка адаптивной карточки. Настроенная `entityId` `tabContext` для вкладки адаптивной карточки отправляется в параметре каждого запроса на вызов и может использоваться для различения вкладок адаптивной карточки, которые используются на основе одного бота. Дополнительные сведения о других полях определения статических вкладок см. в [схеме манифеста](../../resources/schema/manifest-schema.md#statictabs).

Ниже приведен пример манифеста вкладки адаптивной карточки:

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

Обмен данными между вкладкой адаптивной карточки и ботом осуществляется с помощью действий `invoke` . Каждое `invoke` действие имеет соответствующее **имя**. Используйте имя каждого действия, чтобы различать каждый запрос. `tab/fetch` и `tab/submit` действия, описанные в этом разделе.

> [!NOTE]
>
> * Боты должны отправлять все ответы на [URL-адрес службы](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true). URL-адрес службы получается в составе входящих полезных `activity` данных.
> * Размер полезных данных вызова увеличен до 80 КБ.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Получение адаптивной карточки для отрисовки на вкладке

`tab/fetch` — это первый запрос на вызов, который бот получает, когда пользователь открывает вкладку адаптивной карточки. Когда бот получает запрос, он отправляет ответ tab **continue** или ответ проверки **подлинности вкладки** .
Ответ **"** Продолжить" включает массив **для карточек**, который отображается вертикально на вкладке в порядке массива.

> [!NOTE]
> Дополнительные сведения об **ответе проверки подлинности** см. [в разделе проверки подлинности](#authentication).

В следующем коде приведены примеры запросов `tab/fetch` и ответов.

**`tab/fetch` Запрос**

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

**`tab/fetch` Ответ**

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

### <a name="handle-submits-from-adaptive-card"></a>Обработка отправки из адаптивной карточки

После отрисовки адаптивной карточки на вкладке она может реагировать на действия пользователя. Этот ответ обрабатывается запросом на `tab/submit` вызов.

Когда пользователь нажмет кнопку на вкладке адаптивной карточки, `tab/submit` `Action.Submit` запрос будет активироваться к боту с соответствующими данными с помощью функции адаптивной карточки. Данные адаптивной карточки доступны через свойство данных запроса `tab/submit` . Вы получите один из следующих ответов на ваш запрос:

* Ответ кода состояния `200` HTTP без текста. Пустой ответ 200 приводит к отсутствию действий, выполняемых клиентом.
* Ответ на стандартную `200` **вкладку "Продолжить** ", как описано в разделе ["Выбор адаптивной карточки"](#fetch-adaptive-card-to-render-to-a-tab). Ответ на **вкладку "** Продолжить" активирует клиент для обновления отрисовки адаптивной карточки с помощью адаптивных карточек, указанных в массиве карточек ответа **"Продолжить** ".

В следующем коде приведены примеры запросов `tab/submit` и ответов.

**`tab/submit` Запрос**

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

**`tab/submit` Ответ**

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

## <a name="understand-task-module-workflow"></a>Общие сведения о рабочем процессе модуля задач

Модуль задач также использует адаптивную карточку для вызова `task/fetch` , запросов `task/submit` и ответов. Дополнительные сведения см. в статье об использовании модулей задач [в Microsoft Teams ботов](../../task-modules-and-cards/task-modules/task-modules-bots.md).

С появлением вкладки адаптивной карточки изменяется способ ответа бота на запрос `task/submit` . Если вы используете вкладку адаптивной карточки, `task/submit` бот отвечает на запрос на вызов, используя стандартный ответ на вкладку "Продолжить", и закрывает модуль задачи. Вкладка "Адаптивная карточка" обновляется путем отображения нового списка карточек, указанных в тексте ответа **"** Продолжить вкладку".

### <a name="invoke-taskfetch"></a>Вызова `task/fetch`

В следующем коде приведены примеры запросов `task/fetch` и ответов.

**`task/fetch` Запрос**

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

**`task/fetch` Ответ**

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

### <a name="invoke-tasksubmit"></a>Вызова `task/submit`

В следующем коде приведены примеры запросов `task/submit` и ответов.

**`task/submit` Запрос**

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

**`task/submit` Тип ответа табуляции**

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

В предыдущих разделах вы видели, что большинство парадигм разработки можно расширить из запросов и ответов модуля задач в запросы и ответы на вкладку. При обработке проверки подлинности рабочий процесс для вкладки адаптивной карточки следует шаблону проверки подлинности для расширений сообщений. Дополнительные сведения см. в [разделе "Добавление проверки подлинности"](../../messaging-extensions/how-to/add-authentication.md).

`tab/fetch` Запросы  могут иметь **либо продолжение,** либо ответ **проверки подлинности** . Когда запрос `tab/fetch` активируется и получает ответ проверки подлинности  вкладки, пользователю отображается страница входа.

**Получение кода проверки подлинности с помощью вызова `tab/fetch`**

1. Откройте приложение. Появится страница входа.

    > [!NOTE]
    > Логотип приложения предоставляется через свойство `icon` , определенное в манифесте приложения. Заголовок, отображаемый после определения логотипа `title` в свойстве, возвращаемом в тексте ответа **проверки подлинности** вкладки.

1. Щелкните ссылку **Войти**. Вы будете перенаправлены на URL-адрес проверки подлинности, указанный `value` в свойстве текста ответа **проверки** подлинности.
1. Открывается всплывающее окно. В этом всплывающем окне веб-страница размещается по URL-адресу проверки подлинности.
1. После входа закройте окно. Код **проверки подлинности** отправляется Teams клиента.
1. Затем Teams повторно выполняет `tab/fetch` запрос к службе, который включает код проверки подлинности, предоставленный размещенной веб-страницей.

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` поток данных проверки подлинности

На следующем рисунке представлен обзор работы потока данных проверки подлинности для вызова `tab/fetch` .

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Пример потока проверки подлинности адаптивной карточки." border="false":::

**`tab/fetch` Ответ проверки подлинности**

В следующем коде приведен пример ответа проверки `tab/fetch` подлинности:

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

В следующем коде показан пример повторно выданного запроса:

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
| Отображение адаптивных карточек на Teams вкладке | Microsoft Teams пример кода вкладки, в котором показано, как отображать адаптивные карточки в Teams. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Предварительный просмотр для ссылки "Вкладки" и представление стадий](~/tabs/tabs-link-unfurling.md)

## <a name="see-also"></a>См. также

* [Адаптивная карточка](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Teams вкладок](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Отзывы о завершении формы](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
