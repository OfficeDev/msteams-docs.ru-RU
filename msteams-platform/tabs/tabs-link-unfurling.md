---
title: Развертывание ссылок вкладок и представление "Экран"
author: Rajeshwari-v
description: Сведения о представлении стадии— полноэкранном компоненте пользовательского интерфейса, вызываемом для вывода веб-содержимого. Размыкание ссылок используется для того, чтобы преобразовать URL-адреса в вкладку с помощью адаптивных карточек.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: c11e65958e14db8f29206ff3585680818c18c5af
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027293"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Предварительный просмотр для ссылки "Вкладки" и представление стадий

Представление стадии — это новый компонент пользовательского интерфейса. Он позволяет отобразить содержимое, открытое в Полноэкранном режиме в Teams и закрепленное как вкладка.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="stage-view"></a>Представление "Экран"

Представление "Экран" — это компонент полноэкранного пользовательского интерфейса, который можно вызвать для отображения веб-содержимого. Существующая служба размыкания ссылок обновляется таким образом, чтобы она использовалась для включения URL-адресов в вкладку с помощью адаптивных карточек и служб чата. Когда пользователь отправляет URL-адрес в чате или канале, URL-адрес развертывается в адаптивную карточку. Пользователь может выбрать **Просмотр** в карточке и закрепить содержимое как вкладку непосредственно в представлении "Экран".

## <a name="advantage-of-stage-view"></a>Преимущество представления "Экран"

Stage View helps provide a more seamless experience of viewing content in Teams. Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access leading to a higher user engagement with your app.

## <a name="stage-view-vs-task-module"></a>Представление "Экран" в сравнении с модулем задач

|Представление "Экран"|Модуль задач|
|:-----------|:-----------|
|Представление "Экран" удобно использовать, если у вас есть форматированное содержимое, которое нужно показать пользователям, например страница, панель мониторинга, файл и т. д. Он предоставляет широкие возможности, которые помогают отрисовке содержимого на холсте полноэкранного просмотра.|[Модуль задач](../task-modules-and-cards/task-modules/task-modules-tabs.md) особенно удобен для отображения сообщений, которые требуют внимания пользователя, или сбора сведений, необходимых для перехода к следующему шагу.|
  
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

* When the user selects **View**, the bot receives an `invoke` request. The request type is `composeExtension/queryLink`.
* Отклик `invoke` от бота содержит адаптивную карточку с типом `tab/tabInfoAction`.
* Бот отвечает кодом `200`.

> [!NOTE]
>
> On Teams mobile clients, invoking Stage View for apps distributed through the [Teams store](~/concepts/deploy-and-publish/apps-publish-overview.md) and not having a moblie-optimized experience opens the default web browser of the device. The browser opens the URL specified in the `websiteUrl` parameter of the `TabInfo` object.

## <a name="invoke-stage-view-through-deep-link"></a>Вызов представления "Экран" через прямую ссылку

Чтобы вызвать представление "Экран" через прямую ссылку на вкладке, необходимо заключить URL-адрес прямой ссылки в API `app.openLink(url)`. Прямую ссылку также можно передать через действие `OpenURL` в карточке.

### <a name="syntax"></a>Синтаксис

Ниже приведен синтаксис глубокой ссылки:

`<https://teams.microsoft.com/l/stage/{appId}/0?context>={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}`

### <a name="examples"></a>Примеры

Когда пользователь вводит URL-адрес, он распаковкается в адаптивную карточку.

Ниже приведены примеры прямых ссылок для вызова представления "Экран".

**Пример 1. URL-адрес с threadId**

Некодированный URL-адрес:

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous","threadId":"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}`

Закодированный URL-адрес:

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D>`

**Пример 2. URL-адрес без threadId**

Некодированный URL-адрес:

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous"}`

Закодированный

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D>`

> [!NOTE]
> Перед вставка URL-адреса необходимо закодировать все глубокие ссылки. Некодированные URL-адреса не поддерживаются.
>
> * Параметр `name` необязателен в прямой ссылке. Если он не указан, его заменяет имя приложения.
> * Прямую ссылку также можно передать через действие `OpenURL`.
> * При запуске экрана из определенного контекста убедитесь, что ваше приложение работает в этом контексте. Например, если представление "Экран" запускается из личного приложения, у вашего приложения должна быть личная область.

## <a name="tab-information-property"></a>Свойство сведений о вкладке

| Имя свойства | Тип | Число знаков | Описание |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | Это свойство является уникальным идентификатором объекта, отображаемого вкладкой. Это поле обязательно для заполнения.|
| `name` | String | 128 | Это свойство является отображаемым именем вкладки в интерфейсе канала. Это поле является необязательным.|
| `contentUrl` | String | 2048 | This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas. This is a required field.|
| `websiteUrl?` | String | 2048 | This property is the https:// URL to point at, if a user selects to view in a browser. This is a required field.|
| `removeUrl?` | String | 2048 | Это свойство является URL-адресом (https://), указывающим на пользовательский интерфейс, который отображается при удалении вкладки пользователем. Это необязательное поле.|

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | C# |Node.js|
|-------------|-------------|------|----|
|Вкладка в представлении "Экран" |Пример приложения со вкладкой Microsoft Teams для демонстрации вкладки в представлении "Экран".|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание вкладок бесед](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Развертывание ссылок в расширениях для сообщений](~/messaging-extensions/how-to/link-unfurling.md)
* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
