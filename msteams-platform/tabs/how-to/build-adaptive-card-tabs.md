---
title: Создание вкладок адаптивной карточки
author: KirtiPereira
description: Узнайте, как создавать вкладки с помощью адаптивных карточек, где внешний интерфейс отрисовка выполняется с помощью адаптивных карточек. Серверная часть использует бот. Изучение действий вызова и обработка отправки.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: c69ca5f366e973fcd17e04ef490514526bef0f96
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499288"
---
# <a name="build-tabs-with-adaptive-cards"></a>Создание вкладок с использованием адаптивных карточек

> [!IMPORTANT]
>
> Вкладки с адаптивными карточками в настоящее время поддерживаются только в качестве личных приложений.

При разработке вкладки с помощью традиционного метода могут возникнуть следующие проблемы.

* Вопросы HTML и CSS
* Длительная загрузка
* Ограничения iFrame
* Обслуживание и затраты сервера

Вкладки адаптивной карточки — это новый способ создания вкладок в Teams. Вместо внедрения веб-содержимого в iFrame адаптивные карточки можно отобразить на вкладке. При отрисовке внешнего интерфейса с помощью адаптивных карточек серверная часть поддерживается ботом. Бот отвечает за принятие запросов и соответствующий ответ с помощью отрисованной адаптивной карточки.

Вы можете создавать вкладки с помощью готовых рабочих блоков пользовательского интерфейса на компьютере, в Интернете и на мобильных устройствах. Эта статья поможет вам понять, какие изменения необходимо внести в манифест приложения. В этой статье также указывается, как вызов действия запрашивает и отправляет информацию на вкладке с помощью адаптивных карточек, а также влияет на рабочий процесс модуля задач.

На следующем рисунке показаны вкладки сборки с адаптивными карточками на настольных компьютерах и мобильных устройствах.

:::image type="content" source="../../assets/images/adaptive-cards-rendered-in-tabs.png" alt-text="Пример адаптивной карточки, отрисованной на вкладках.":::

## <a name="prerequisites"></a>Предварительные условия

Прежде чем приступить к созданию вкладок с помощью адаптивных карточек, необходимо сделать следующее.

* Ознакомьтесь с [разработкой ботов](../../bots/what-are-bots.md), [адаптивными карточками](https://adaptivecards.io/) и [модулями задач](../../task-modules-and-cards/task-modules/task-modules-bots.md) в Teams.
* Для разработки в Teams должен быть запущен бот.

## <a name="changes-to-app-manifest"></a>Изменения манифеста приложения

Личные приложения, которые отрисовывают вкладки, должны включать массив `staticTabs` в манифест приложения. Вкладки адаптивной карточки отрисовываются, когда свойство `contentBotId` предоставляется в определении `staticTab`. Определения статических вкладок должны содержать либо `contentBotId`, указывая вкладку адаптивной карточки, либо `contentUrl`, указывая типичную вкладку с веб-содержимым.

> [!NOTE]
> Свойство `contentBotId` в настоящее время доступно в манифесте версии 1.9 или более поздних версиях.

Предоставьте свойству `contentBotId` `botId`, с которым адаптивная карточка должна взаимодействовать. Класс `entityId` настроенный для вкладки адаптивной карточки, отправляется в параметре `tabContext` каждого запроса на вызов и может использоваться для различения вкладок адаптивной карточки, которые работают на основе одного бота. Дополнительные сведения о других полях определения статических вкладок см. в статье [Схема манифеста](../../resources/schema/manifest-schema.md#statictabs).

Ниже приводится пример манифеста вкладки адаптивной карточки:

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "1.9",
  "id": "00000000-0000-0000-0000-000000000000",
  "version": "0.0.1",
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

## <a name="invoke-activities"></a>Запуск действия

Связь между вкладкой адаптивной карточки и ботом реализуется через действия — `invoke`. Каждое действие `invoke` имеет соответствующее **имя**. Используйте имена каждого действия для различения каждого запроса. `tab/fetch` и `tab/submit` — это действия, которые охватываются в этом разделе.

> [!NOTE]
>
> * Ботам необходимо отправлять все ответы на [URL-адрес службы](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true). URL-адрес службы получен в составе входящей полезной нагрузки `activity`.
> * Размер полезной нагрузки вызова увеличен до 80 КБ.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Извлечение адаптивной карточки для отрисовки на вкладке

`tab/fetch` — это первый запрос на вызов, который ваш бот получает, когда пользователь открывает вкладку адаптивной карточки. Когда бот получает запрос, он отправляет ответ о **продолжении** или вкладку **аутетификация** в ответ.
Ответ **continue** включает массив для **карточек**, который отображается вертикально вкладке в другом массиве.

> [!NOTE]
> Дополнительные сведения об ответе **auth** см. в разделе [Проверка подлинности](#authentication).

Следующий код содержит примеры запроса `tab/fetch` и ответа:

**`tab/fetch`: запрос**

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

**`tab/fetch`: отклик**

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

### <a name="handle-submits-from-adaptive-card"></a>Обработка отправок с адаптивной карточки

После отрисовки адаптивной карточки на вкладке она может реагировать на действия пользователей. Этот ответ обрабатывается запросом на вызов `tab/submit`.

Когда пользователь нажал кнопку на вкладке адаптивной карточки, запрос `tab/submit` запускается к боту с соответствующими данными через функцию `Action.Submit` адаптивной карточки. Данные адаптивной карточки доступны через свойство данных запроса `tab/submit`. Вы получите один из следующих ответов на ваш запрос:

* Код состояния HTTP `200` не имеет тела. Две сотни пустых ответов не приводит к никаким действиям клиента.
* Стандартная `200` вкладка **continue** отвечать, как объяснено в разделе [Адаптивная карточка](#fetch-adaptive-card-to-render-to-a-tab). Отклик вкладки **continue** активирует клиента, чтобы обновить отрисовку адаптивной карточки с помощью адаптивных карточек, предоставленных в массиве карточек отклика **continue**.

Следующий код содержит примеры запроса `tab/submit` и ответа:

**`tab/submit`: запрос**

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

**`tab/submit`: отклик**

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

## <a name="understand-task-module-workflow"></a>Сведения о рабочем процессе модуля задач

Модуль задач также использует адаптивную карточку для вызова запросов и ответов `task/fetch` и `task/submit`. Подробнее в разделе [об использовании модулей задач в ботах Microsoft Teams](../../task-modules-and-cards/task-modules/task-modules-bots.md).

С появлением вкладки "Адаптивная карточка" изменилось то, как бот отвечает на запрос `task/submit`. Если вы используете вкладку адаптивной карточки, бот отвечает на запрос вызова `task/submit` стандартной вкладкой **continue** и закрывает модуль задач. Вкладка "Адаптивная карточка" обновляется путем отрисовки нового списка карточек, предоставленных в основной части отклика на вкладке **continue**.

### <a name="invoke-taskfetch"></a>Вызов `task/fetch`

Следующий код содержит примеры запроса `task/fetch` и ответа:

**`task/fetch`: запрос**

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

**`task/fetch`: отклик**

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

Следующий код содержит примеры запроса `task/submit` и ответа:

**`task/submit`: запрос**

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

**`task/submit`: тип ответа вкладки**

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

В предыдущих разделах вы видели, что большинство стратегий разработки можно расширить из запросов модуля задач и ответов на запросы и ответы вкладки. При обработке проверки подлинности рабочий процесс для вкладки адаптивной карточки следует шаблону проверки подлинности расширений для сообщений. Дополнительные сведения см. в статье [о добавлении проверки подлинности](../../messaging-extensions/how-to/add-authentication.md).

Запросы `tab/fetch` могут иметь ответ **continue** или **auth**. Когда запрос `tab/fetch` запускается и получает в ответ вкладку **auth**, пользователю отображается страница входа.

**Получение кода проверки подлинности через вызов `tab/fetch`**

1. Откройте приложение. Появится страница входа.

    > [!NOTE]
    > Логотип приложения предоставляется через свойство `icon`, определенное в манифесте приложения. Заголовок, который появляется после определения логотипа в свойстве `title`, возвращаемом в теле ответа **auth**.

1. Щелкните ссылку **Войти**. Вы будете перенаправлены на URL-адрес проверки подлинности, предоставленный в свойстве `value` в теле ответа **auth**.
1. Открывается всплывающее окно. Это всплывающее окно размещено на веб-странице с использованием URL-адреса проверки подлинности.
1. После входа закройте окно. **Код проверки подлинности** отправляется в клиент Teams.
1. Затем клиент Teams повторно передает запрос `tab/fetch` службе, которая включает код проверки подлинности, предоставленный вашей веб-страницей.

### <a name="tabfetch-authentication-data-flow"></a>Поток данных проверки подлинности `tab/fetch`

На следующем изображении представлен обзор работы потока данных проверки подлинности для вызова `tab/fetch`.

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Пример автоматического потока вкладки &quot;Адаптивная карточка&quot;.":::

**`tab/fetch`: ответ auth**

Этот фрагмент программного кода представляет собой пример ответа на проверку подлинности `tab/fetch`:

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

В следующем коде показан пример повторной выдачи запроса:

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
| Показывать адаптивные карточки на вкладке Teams | Образец кода вкладки Microsoft Teams, в котором показано, как показывать адаптивные карточки в Teams. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Развертывание ссылок вкладок и представление "Экран"](~/tabs/tabs-link-unfurling.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Адаптивная карточка](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Отзывы о завершении формы](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
