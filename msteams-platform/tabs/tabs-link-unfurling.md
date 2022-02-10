---
title: Предварительный просмотр для ссылки "Вкладки" и представление стадий
author: Rajeshwari-v
description: Узнайте, как развязать ссылку, открыть представление сцены и закрепить вкладку с помощью Microsoft Teams приложения. Узнайте о представлении сцены и его наводке с помощью адаптивной карты с помощью примера кода и примера.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 48c7ae69b10702d58be933b5619fd6bdeb8cecf3
ms.sourcegitcommit: 3332ca6f61d2d60ddb20140f6d163905ea177157
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/10/2022
ms.locfileid: "62516521"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Предварительный просмотр для ссылки "Вкладки" и представление стадий

Представление stage — это новый компонент пользовательского интерфейса (пользовательского интерфейса), который позволяет отрисовки контента, открываемой на полном экране в Teams и закрепленной в качестве вкладки.
 
## <a name="stage-view"></a>Представление сцены

Представление stage — это компонент пользовательского интерфейса полного экрана, который можно вызвать для поверхности веб-контента. Существующая служба разгрузки ссылок обновляется таким образом, чтобы она использовалась для того, чтобы превратить URL-адреса в вкладку с помощью служб адаптивной карты и чата. Когда пользователь отправляет URL-адрес в чате или канале, URL-адрес будет развернут на адаптивную карту. Пользователь может выбрать **Просмотр** на карте и закрепить содержимое в качестве вкладки непосредственно из представления stage.

## <a name="advantage-of-stage-view"></a>Преимущество представления на этапе

Представление stage позволяет обеспечить более бесперебойное просмотр контента в Teams. Пользователи могут открывать и просматривать контент, предоставляемый вашим приложением, не выходя из контекста, и могут прикрепить содержимое к чату или каналу для быстрого доступа к будущему, что приводит к более высокому взаимодействию пользователя с вашим приложением.

## <a name="stage-view-vs-task-module"></a>Модуль Представления сцены и задачи

|Представление сцены|Модуль задач|
|:-----------|:-----------|
|Представление stage полезно, если у вас есть богатый контент для отображения для пользователей, таких как страница, панель мониторинга, файл и так далее. Он предоставляет богатые функции, которые помогают отрисовки контента на полноэкранной холсте.|[Модуль задач](../task-modules-and-cards/task-modules/task-modules-tabs.md) особенно полезен для отображения сообщений, которые требуют внимания пользователя, или сбора сведений, необходимых для перемещения на следующий шаг.|
  
## <a name="invoke-stage-view"></a>Вызов представления стадии

Вы можете вызвать представление stage следующим образом:

* [Вызов представления сцены из адаптивной карты](#invoke-stage-view-from-adaptive-card)
* [Вызов представления сцены по глубокой ссылке](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>Вызов представления сцены из адаптивной карты

Когда пользователь вводит URL-адрес Teams настольного клиента, бот вызывается и возвращает адаптивную карту с возможностью открытия URL-адреса на этапе.[](../task-modules-and-cards/cards/cards-actions.md) После запуска этапа и `tabInfo` предоставляются, можно добавить возможность закрепить этап в качестве вкладки.  

На следующих изображениях показан этап, открытый с адаптивной карты:

[![Откройте этап из адаптивной карты](~/assets/images/tab-images/open-stage-from-adaptive-card1.png)](~/assets/images/tab-images/open-stage-from-adaptive-card1.png#lightbox)

[![Откройте этап](~/assets/images/tab-images/open-stage-from-adaptive-card2.png)](~/assets/images/tab-images/open-stage-from-adaptive-card2.png#lightbox) 

### <a name="example"></a>Пример

Ниже приводится код, который откроет этап с адаптивной карты:

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

Тип `invoke` запроса должен быть `composeExtension/queryLink`.

> [!NOTE]
> * `invoke` рабочий процесс похож на текущий `appLinking` рабочий процесс. 
> * Для обеспечения согласованности рекомендуется `Action.Submit` назвать как `View`.
> * `websiteUrl` это обязательное свойство, передав его объекту `TabInfo` .

Ниже приводится процесс вызова представления stage:

* Когда пользователь выбирает **View**, бот получает запрос `invoke` . Тип запроса `composeExtension/queryLink`.
* `invoke` Ответ от бота содержит адаптивную карточку с типом `tab/tabInfoAction` в ней.
* Бот отвечает кодом `200` .

> [!NOTE]
> В Teams мобильных клиентов, привнося представление stage View для приложений, [распространяемых через Teams](/platform/concepts/deploy-and-publish/apps-publish-overview.md) магазина и не имеющих оптимизированного для мобли опыта, открывает веб-браузер устройства по умолчанию. Браузер открывает URL-адрес, указанный в `websiteUrl` параметре `TabInfo` объекта.

## <a name="invoke-stage-view-through-deep-link"></a>Вызов представления сцены по глубокой ссылке

Чтобы вызвать представление стадии с помощью глубокой ссылки на вкладке, необходимо завернуть URL-адрес глубокой ссылки в `microsoftTeams.executeDeeplink(url)` API. Глубокая ссылка также может быть передана через действие `OpenURL` в карточке.

### <a name="syntax"></a>Синтаксис

Ниже приводится синтаксис deeplink: 

https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}
 
### <a name="examples"></a>Примеры

Когда пользователь вводит URL-адрес, он будет развернут в адаптивную карту.

Ниже приводятся примеры глубоких ссылок для вызова представления stage:

**Пример 1**

Не закодированы
 
https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx",websiteUrl:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name":"Contoso"}

Закодированная

https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context=%7B%22contentUrl%22%3A%22https%253A%252F%252Fmicrosoft.sharepoint.com%252Fteams%252FLokisSandbox%252FSitePages%252FSandbox-Page.aspx%22%2C%22websiteUrl%0A%3A%22https%253A%252F%252Fmicrosoft.sharepoint.com%252Fteams%252FLokisSandbox%252FSitePages%252FSandbox-Page.aspx%22%2C%22name%22%3A%22Contoso%22%7D


**Пример 2**

Не закодированы

https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":""https://microsoft.sharepoint.com/teams/LokisSandbox/SitePages/Sandbox-Page.aspx,"websiteUrl":""https://microsoft.sharepoint.com/teams/LokisSandbox/SitePages/Sandbox-Page.aspx,name":"Contoso"}

Закодированная

https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx%22%2C%22name%22%3A%22Contoso%22%7D


> [!NOTE]
> Все глубокие ссылки должны быть закодированы перед вклейкой URL-адреса. Мы не поддерживаем некодированные URL-адреса.
> * Необязательный `name` в глубокой ссылке. Если оно не включено, имя приложения заменяет его.
> * Глубокая ссылка также может быть передана через `OpenURL` действие.
> * При запуске stage из определенного контекста убедитесь, что приложение работает в этом контексте. Например, если представление stage запущено из личного приложения, необходимо убедиться, что ваше приложение имеет личную область.

## <a name="tab-information-property"></a>Свойство сведений tab

| Имя свойства | Тип | Количество символов | Описание |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | Это свойство является уникальным идентификатором для объекта, отображаемого на вкладке. Это поле обязательно для заполнения.|
| `name` | String | 128 | Это свойство — отображаемая вкладки в интерфейсе канала. Это поле является необязательным.|
| `contentUrl` | String | 2048 | Это свойство — https:// URL-адрес, который указывает на пользовательский интерфейс объекта, отображаемого на Teams холсте. Это поле обязательно для заполнения.|
| `websiteUrl?` | String | 2048 | Это свойство является https://, на который нужно указать, если пользователь выбирает для просмотра в браузере. Это поле обязательно для заполнения.|
| `removeUrl?` | String | 2048 | Это свойство — https:// URL-адрес, который указывает на пользовательский интерфейс, который будет отображаться при удалении вкладки пользователем. Это необязательное поле.|

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | C# |Node.js|
|-------------|-------------|------|----|
|Вкладка в представлении сцены |Microsoft Teams пример приложения вкладки для демонстрации вкладки в представлении сцены.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|
    

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладок бесед](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>См. также

* [Расширение обмена сообщениями связывает разгрузку](~/messaging-extensions/how-to/link-unfurling.md)
* [Teams вкладки](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
