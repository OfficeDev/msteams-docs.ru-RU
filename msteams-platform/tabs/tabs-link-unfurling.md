---
title: Развертывание ссылок вкладок и представление "Экран"
author: Rajeshwari-v
description: Узнайте, как развернуть ссылку, открыть представление "Экран" и закрепить вкладку с приложением Microsoft Teams. Сведения о представлении "Экран" и его вызове с помощью адаптивной карточки с использованием примера кода и образца.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: medium
ms.openlocfilehash: 08df4cfccf6d9fabad1e07736796d6728d7c527c
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756739"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Развертывание ссылок вкладок и представление "Экран"

Представление стадии — это новый компонент пользовательского интерфейса. Он позволяет отображать содержимое, открытое в полноэкранном режиме Teams и закрепленное как вкладка.

## <a name="stage-view"></a>Представление "Экран"

Представление "Экран" — это компонент полноэкранного пользовательского интерфейса, который можно вызвать для отображения веб-содержимого. Существующая служба размыкания ссылок обновляется таким образом, чтобы она использовалась для включения URL-адресов в вкладку с помощью адаптивных карточек и служб чата. Когда пользователь отправляет URL-адрес в чате или канале, URL-адрес развертывается в адаптивную карточку. Пользователь может выбрать **Просмотр** в карточке и закрепить содержимое как вкладку непосредственно в представлении "Экран".

## <a name="advantage-of-stage-view"></a>Преимущество представления "Экран"

Представление сцены помогает обеспечить более удобный просмотр содержимого в Teams. Пользователи могут открывать и просматривать содержимое, предоставленное вашим приложением, не выходя из контекста, и они могут закрепить содержимое в чате или канале для быстрого доступа в будущем, что приведет к более активному взаимодействию пользователей с вашим приложением.

## <a name="stage-view-vs-task-module"></a>Представление "Экран" в сравнении с модулем задач

|Представление "Экран"|Модуль задач|
|:-----------|:-----------|
|Представление "Экран" удобно использовать, если у вас есть форматированное содержимое, которое нужно показать пользователям, например страница, панель мониторинга, файл и т. д. Оно предоставляет широкие возможности отрисовки вашего содержимого на полноэкранном холсте.|[Модуль задач](../task-modules-and-cards/task-modules/task-modules-tabs.md) особенно удобен для отображения сообщений, которые требуют внимания пользователя, или сбора сведений, необходимых для перехода к следующему шагу.|
  
## <a name="invoke-stage-view"></a>Вызов представления "Экран"

Представление "Экран" можно вызвать следующими способами.

* [Вызов представления "Экран" из адаптивной карточки](#invoke-stage-view-from-adaptive-card)
* [Вызов представления "Экран" через прямую ссылку](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>Вызов представления "Экран" из адаптивной карточки

Когда пользователь вводит URL-адрес в классическом клиенте Teams, вызывается бот, который возвращает [адаптивную карточку](../task-modules-and-cards/cards/cards-actions.md) с возможностью открыть URL-адрес на экране. После запуска экрана и предоставления `tabInfo` вы можете добавить возможность закрепить экран как вкладку.  

На следующих изображениях показан экран, открытый из адаптивной карточки.

[![Открытие экрана из адаптивной карточки](~/assets/images/tab-images/open-stage-from-adaptive-card1.png)](~/assets/images/tab-images/open-stage-from-adaptive-card1.png#lightbox)

[![Открытие экрана](~/assets/images/tab-images/open-stage-from-adaptive-card2.png)](~/assets/images/tab-images/open-stage-from-adaptive-card2.png#lightbox)

### <a name="example"></a>Пример

Ниже приведен код для открытия экрана из адаптивной карточки.

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

Типом запроса `invoke` должен быть `composeExtension/queryLink`.

> [!NOTE]
>
> * Рабочий процесс `invoke` аналогичен текущему рабочему процессу `appLinking`.
> * Для обеспечения согласованности рекомендуется присвоить для `Action.Submit` имя `View`.
> * `websiteUrl` является обязательным свойством, которое передается в объекте `TabInfo`.

Ниже приведен процесс вызова представления "Экран".

* Когда пользователь выбирает **Просмотр**, бот получает запрос `invoke`. Тип запроса `composeExtension/queryLink`.
* Отклик `invoke` от бота содержит адаптивную карточку с типом `tab/tabInfoAction`.
* Бот отвечает кодом `200`.

> [!NOTE]
> В мобильных клиентах Teams вызов представления Stage для приложений, распространяемых через [Teams store](/platform/concepts/deploy-and-publish/apps-publish-overview.md) и не оптимизированных для мобильных устройств, открывает веб-браузер устройства по умолчанию. Браузер открывает URL-адрес, указанный в параметре `websiteUrl` объекта `TabInfo`.

## <a name="invoke-stage-view-through-deep-link"></a>Вызов представления "Экран" через прямую ссылку

Чтобы вызвать представление "Экран" через прямую ссылку на вкладке, необходимо заключить URL-адрес прямой ссылки в API `microsoftTeams.executeDeeplink(url)`. Прямую ссылку также можно передать через действие `OpenURL` в карточке.

### <a name="syntax"></a>Синтаксис

Ниже приведен синтаксис прямой ссылки.

https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}
 
### <a name="examples"></a>Примеры

Когда пользователь вводит URL-адрес, он распаковкается в адаптивную карточку.

Ниже приведены примеры прямых ссылок для вызова представления "Экран".

**Пример 1. URL-адрес с threadId**

Некодированный URL-адрес:

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191,"websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true,"title":"Quotes: Miscellaneous","threadId":"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}

Закодированный URL-адрес:

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D

**Пример 2. URL-адрес без threadId**

Некодированный URL-адрес:

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context={"contentUrl":",https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191"websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true,"title":"Quotes: Miscellaneous"}

Закодированный

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D

> [!NOTE]
> Перед вставкой URL-адреса необходимо закодировать все прямые ссылки. Некодированные URL-адреса не поддерживаются.
>
> * Параметр `name` необязателен в прямой ссылке. Если он не указан, его заменяет имя приложения.
> * Прямую ссылку также можно передать через действие `OpenURL`.
> * При запуске экрана из определенного контекста убедитесь, что ваше приложение работает в этом контексте. Например, если представление "Экран" запускается из личного приложения, у вашего приложения должна быть личная область.

## <a name="tab-information-property"></a>Свойство сведений о вкладке

| Имя свойства | Тип | Число знаков | Описание |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | Это свойство является уникальным идентификатором объекта, отображаемого вкладкой. Это поле обязательно для заполнения.|
| `name` | String | 128 | Это свойство является отображаемым именем вкладки в интерфейсе канала. Это поле является необязательным.|
| `contentUrl` | String | 2048 | Это свойство представляет собой URL-адрес https://, указывающий на пользовательский интерфейс объекта, который будет отображаться на холсте Teams. Это поле обязательно для заполнения.|
| `websiteUrl?` | String | 2048 | Это свойство представляет собой URL-адрес https://, на который нужно указать, если пользователь выбирает просмотр в браузере. Это поле обязательно для заполнения.|
| `removeUrl?` | String | 2048 | Это свойство является URL-адресом (https://), указывающим на пользовательский интерфейс, который отображается при удалении вкладки пользователем. Это необязательное поле.|

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | C# |Node.js|
|-------------|-------------|------|----|
|Вкладка в представлении "Экран" |Пример приложения со вкладкой Microsoft Teams для демонстрации вкладки в представлении "Экран".|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладок бесед](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Развертывание ссылок в расширениях для сообщений](~/messaging-extensions/how-to/link-unfurling.md)
* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
