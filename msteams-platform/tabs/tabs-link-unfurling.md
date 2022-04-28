---
title: Предварительный просмотр для ссылки "Вкладки" и представление стадий
author: Rajeshwari-v
description: Узнайте, как распаковка ссылки, открытие представления стадии и закрепление вкладки с Microsoft Teams приложения. Сведения о представлении стадии и вызове его с помощью адаптивной карточки с помощью примера кода и примера.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 043129d6a81543ac00acf8b64da49f75282823a2
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104086"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Предварительный просмотр для ссылки "Вкладки" и представление стадий

Представление стадии — это новый компонент пользовательского интерфейса, который позволяет отображать содержимое, открытое в полноэкранном режиме Teams и закрепленное как вкладка.

## <a name="stage-view"></a>Представление стадии

Представление стадии — это полноэкранный компонент пользовательского интерфейса, который можно вызвать для просмотра веб-содержимого. Существующая служба размыкания ссылок обновляется таким образом, чтобы она использовалась для включения URL-адресов в вкладку с помощью адаптивных карточек и служб чата. Когда пользователь отправляет URL-адрес в чате или канале, URL-адрес распакается на адаптивную карточку. Пользователь может выбрать " **Вид** " в карточке и закрепить содержимое как вкладку непосредственно в представлении стадии.

## <a name="advantage-of-stage-view"></a>Преимущество представления стадии

Представление стадии помогает более удобно просматривать содержимое в Teams. Пользователи могут открывать и просматривать содержимое, предоставленное вашим приложением, не выходя из контекста, и закреплять содержимое в чате или канале для быстрого доступа в будущем, что приводит к более высокому вовлечению пользователей в ваше приложение.

## <a name="stage-view-vs-task-module"></a>Представление стадии и модуль задач

|Представление стадии|Модуль задач|
|:-----------|:-----------|
|Представление стадии удобно использовать, если у вас есть полнофункциональный контент для отображения пользователям, например страница, панель мониторинга, файл и т. д. Она предоставляет широкие возможности, которые помогают отрисовке содержимого на холсте полноэкранного просмотра.|[Модуль задач](../task-modules-and-cards/task-modules/task-modules-tabs.md) особенно полезен для отображения сообщений, которые требуют внимания пользователя, или сбора сведений, необходимых для перехода к следующему шагу.|
  
## <a name="invoke-stage-view"></a>Вызов представления стадии

Представление стадии можно вызвать следующими способами:

* [Вызов представления стадии из адаптивной карточки](#invoke-stage-view-from-adaptive-card)
* [Вызов представления стадии через прямую ссылку](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>Вызов представления стадии из адаптивной карточки

Когда пользователь вводит URL-адрес на настольном клиенте Teams, бот вызывается и возвращает адаптивную карточку с возможностью открыть URL-адрес на этапе.[](../task-modules-and-cards/cards/cards-actions.md) После запуска этапа и `tabInfo` предоставления его можно добавить возможность закрепить этап как вкладку.  

На следующих изображениях показан этап, открытый из адаптивной карточки:

[![Открытие этапа из адаптивной карточки](~/assets/images/tab-images/open-stage-from-adaptive-card1.png)](~/assets/images/tab-images/open-stage-from-adaptive-card1.png#lightbox)

[![Открытие этапа](~/assets/images/tab-images/open-stage-from-adaptive-card2.png)](~/assets/images/tab-images/open-stage-from-adaptive-card2.png#lightbox)

### <a name="example"></a>Пример

Ниже приведен код для открытия этапа из адаптивной карточки:

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

Тип `invoke` запроса должен быть .`composeExtension/queryLink`

> [!NOTE]
>
> * `invoke` рабочий процесс аналогичен текущему `appLinking` рабочему процессу.
> * Для поддержания согласованности рекомендуется использовать имя `Action.Submit` `View`..
> * `websiteUrl` является обязательным свойством, которое передается в объекте `TabInfo` .

Ниже приведен процесс вызова представления стадии.

* Когда пользователь выбирает **представление**, бот получает запрос `invoke` . Тип запроса — `composeExtension/queryLink`..
* `invoke` Ответ от бота содержит адаптивную карточку с типом `tab/tabInfoAction` .
* Бот отвечает кодом `200` .

> [!NOTE]
> На Teams мобильных клиентов вызов представления стадии для приложений, [распространяемых](/platform/concepts/deploy-and-publish/apps-publish-overview.md) через хранилище Teams и не имеющих оптимизированного для moblie интерфейса, открывает веб-браузер устройства по умолчанию. Браузер открывает URL-адрес, указанный в параметре `websiteUrl` `TabInfo` объекта.

## <a name="invoke-stage-view-through-deep-link"></a>Вызов представления стадии через прямую ссылку

Чтобы вызвать представление стадии через прямую ссылку на вкладке, необходимо заключить URL-адрес глубокой ссылки в `microsoftTeams.executeDeeplink(url)` API. Прямую ссылку также можно передать через действие `OpenURL` в карточке.

### <a name="syntax"></a>Синтаксис

Ниже приведен синтаксис deeplink:

https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}
 
### <a name="examples"></a>Примеры

Когда пользователь вводит URL-адрес, он распаковкается в адаптивную карточку.

Ниже приведены примеры прямых ссылок для вызова представления стадии:

**Пример 1. URL-адрес с threadId**

Некодированный URL-адрес:

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context={"contentUrl":","https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true,"title":"Quotes:Miscellaneous","threadId":"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}

Закодированный URL-адрес:

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D

**Пример 2. URL-адрес без threadId**

Некодированный URL-адрес:

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context={"contentUrl":",https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191"websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true,"title":"Quotes:Miscellaneous"}

Закодированные

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D

> [!NOTE]
> Перед вставкой URL-адреса необходимо закодировать все прямые ссылки. Мы не поддерживаем некодированные URL-адреса.
>
> * Необязательный `name` параметр в глубокой ссылке. Если этот параметр не включен, имя приложения заменяет его.
> * Прямую ссылку также можно передать через `OpenURL` действие.
> * При запуске этапа из определенного контекста убедитесь, что приложение работает в этом контексте. Например, если представление стадии запускается из личного приложения, необходимо убедиться, что ваше приложение имеет личную область.

## <a name="tab-information-property"></a>Свойство сведений о вкладке

| Имя свойства | Тип | Количество символов | Описание |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | Это свойство является уникальным идентификатором сущности, отображаемой на вкладке. Это поле обязательно для заполнения.|
| `name` | String | 128 | Это свойство представляет собой отображаемое имя вкладки в интерфейсе канала. Это поле является необязательным.|
| `contentUrl` | String | 2048 | Это свойство представляет собой https:// URL-адрес, указывающий на пользовательский интерфейс сущности, отображаемый на Teams холсте. Это поле обязательно для заполнения.|
| `websiteUrl?` | String | 2048 | Это свойство является https:// URL-адресом, на который нужно указать, если пользователь выбирает просмотр в браузере. Это поле обязательно для заполнения.|
| `removeUrl?` | String | 2048 | Это свойство является https:// URL-адресом, указывающим на пользовательский интерфейс, отображаемый при удалении вкладки пользователем. Это необязательное поле.|

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | C# |Node.js|
|-------------|-------------|------|----|
|Вкладка в представлении стадии |Microsoft Teams пример приложения для демонстрации вкладки в представлении этапа.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладок бесед](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>См. также

* [Удаление ссылки на расширения сообщений](~/messaging-extensions/how-to/link-unfurling.md)
* [Teams вкладок](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
