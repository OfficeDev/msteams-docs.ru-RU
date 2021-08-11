---
title: Использование модулей задач в Microsoft Teams вкладками
description: Объясняет, как вызывать модули задач из Teams вкладок с помощью Microsoft Teams SDK клиента.
localization_priority: Normal
ms.topic: how-to
keywords: модули задач группы вкладок sdk клиента
ms.openlocfilehash: 3fe0a20d751b1eb08d70385648be1283a9d9b0c32e5849626df4abd36ba5bdce
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2021
ms.locfileid: "57703585"
---
# <a name="use-task-modules-in-tabs"></a>Использование модулей задач во вкладках

Добавьте модуль задач на вкладку, чтобы упростить работу пользователя для любых процессов, которые требуют ввода данных. Модули задач позволяют собирать входные данные в всплывающее Teams-Aware Microsoft. Хорошим примером этого является редактирование карт Планировщика. Для создания аналогичного опыта можно использовать модули задач.

Чтобы поддерживать функцию модуля задач, в клиентскую [SDK Teams две новые функции.](/javascript/api/overview/msteams-client) В следующем коде показан пример этих двух функций:

```typescript
microsoftTeams.tasks.startTask(
    taskInfo: TaskInfo,
    submitHandler?: (err: string, result: string | any) => void
): void;

microsoftTeams.tasks.submitTask(
    result?: string | any,
    appIds?: string | string[]
): void;
```

Вы можете увидеть, как работает отправка модуля задач со вкладки и отправка результатов работы модуля задач.

## <a name="invoke-a-task-module-from-a-tab"></a>Вызов модуля задач со вкладки

Чтобы вызвать модуль задач со вкладки, используйте передачу объекта `microsoftTeams.tasks.startTask()` [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) и необязательный вызов `submitHandler` функции. Необходимо рассмотреть два случая:

* Значение `TaskInfo.url` установлено для URL-адреса. Окно модуля задач отображается и `TaskModule.url` загружается как `<iframe>` внутреннее. JavaScript на этой странице вызывает `microsoftTeams.initialize()` . Если на странице есть функция и ошибка при вызове, то вызывается с задаваемой строкой ошибки, `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` указывающей то же самое. Дополнительные сведения см. в ссылке на ошибки [вызовов модулей задач.](#task-module-invocation-errors)
* Значение JSON для адаптивной `taskInfo.card` [карты](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). Функция JavaScript не может вызываться при закрытии или нажатии кнопки `submitHandler` на адаптивной карте. Единственный способ получить то, что вошел пользователь, — это передача результата боту. Чтобы использовать модуль задач адаптивной карты со вкладки, приложение должно включить бот, чтобы получить любой ответ от пользователя.

В следующем разделе приводится пример ссылки на модуль задач.

## <a name="example-of-invoking-a-task-module"></a>Пример ссылки на модуль задач

На следующем изображении отображается модуль задач:

![Модуль задач — настраиваемая форма](~/assets/images/task-module/task-module-custom-form.png)

Следующий код адаптируется из [примера модуля задач:](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample)

```javascript
let taskInfo = {
    title: null,
    height: null,
    width: null,
    url: null,
    card: null,
    fallbackUrl: null,
    completionBotId: null,
};

taskInfo.url = "https://contoso.com/teamsapp/customform";
taskInfo.title = "Custom Form";
taskInfo.height = 510;
taskInfo.width = 430;
submitHandler = (err, result) => {
    console.log(`Submit handler - err: ${err}`);
    console.log(`Submit handler - result\rName: ${result.name}\rEmail: ${result.email}\rFavorite book: ${result.favoriteBook}`);
};
microsoftTeams.tasks.startTask(taskInfo, submitHandler);
```

Это `submitHandler` очень просто, и оно повторяет значение `err` консоли или `result` консоли.

## <a name="submit-the-result-of-a-task-module"></a>Отправка результатов модуля задач

Функция `submitHandler` находится на `TaskInfo.url` веб-странице и используется с `TaskInfo.url` . Если при вызове модуля задач возникла ошибка, функция немедленно вызывается строкой, указывающей, какая `submitHandler` `err` ошибка [произошла.](#task-module-invocation-errors) Функция также называется строкой, когда пользователь выбирает X в правом верхнем справа от модуля задач, чтобы `submitHandler` `err` закрыть ее.

Если ошибки вызова нет и пользователь не выбирает X, чтобы отклонять ее, пользователь выбирает кнопку по завершению. В зависимости от url-адреса или адаптивной карты в модуле задач в следующих разделах указаны сведения о том, что происходит.

### <a name="html-or-javascript-taskinfourl"></a>HTML или JavaScript `TaskInfo.url`

После проверки входных данных пользователя вызываем функцию `microsoftTeams.tasks.submitTask()` SDK, которая называется `submitTask()` . Вызов `submitTask()` без параметров, если Teams закрыть модуль задач. Вы можете передать объект или строку в `submitHandler` ваш .

Передай результат в качестве первого параметра. Teams вызывает, где находится и является объект или `submitHandler` `err` `null` строка, которую вы `result` передали `submitTask()` . Если вы `submitTask()` звоните с `result` параметром, необходимо передать или массив `appId` `appId` строк. Это позволяет Teams, что приложение, отправляя результат, является таким же, как и вызываемого модуля задач.

### <a name="adaptive-card-taskinfocard"></a>Адаптивная карта `TaskInfo.card`

Когда вы вызываете модуль задач с помощью кнопки, а пользователь выбирает кнопку, значения в карточке возвращаются в качестве `submitHandler` `Action.Submit` значения `result` . Если пользователь выбирает ключ Esc или X в правом верхнем справа, `err` возвращается вместо него. Если приложение содержит бот в дополнение к вкладке, вы можете просто включить бот в качестве значения `appId` `completionBotId` в `TaskInfo` объекте. Тело адаптивной карты, заполненное пользователем, отправляется боту с помощью сообщения, когда пользователь `task/submit invoke` выбирает `Action.Submit` кнопку. Схема объекта, который вы получаете, очень похожа на схему, которую вы получаете для задач/извлечений и [задач/отправки сообщений.](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages) Единственное отличие состоит в том, что схема объекта JSON является объектом Адаптивной карты, а не объектом, содержащим объект Adaptive Card, как при использования адаптивных карт с [ботами.](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)

В следующем разделе приводится пример отправки результатов модуля задач.

## <a name="example-of-submitting-the-result-of-a-task-module"></a>Пример отправки результата модуля задач

Дополнительные сведения см. в [htmL-форме в модуле задач.](#example-of-invoking-a-task-module) В следующем коде приводится пример определения формы:

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Существует пять полей в этой форме, но для этого примера требуется только три значения, `name` `email` и `favoriteBook` .

В следующем коде приводится пример `validateForm()` функции, которая `submitTask()` вызывает:

```javascript
function validateForm() {
    var customerInfo = {
        name: document.forms["customerForm"]["name"].value,
        email: document.forms["customerForm"]["email"].value,
        favoriteBook: document.forms["customerForm"]["favoriteBook"].value
    }
    microsoftTeams.tasks.submitTask(customerInfo, "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx");
    return true;
}
```

В следующем разделе печатались проблемы с вызовом модулей задач и сообщения об ошибках.

## <a name="task-module-invocation-errors"></a>Ошибки при вызове модуля задач

В следующей таблице возможен доступ к следующим значениям: `err` `submitHandler`

| Проблема | Сообщение об ошибке, значение `err` |
| ------- | ------------------------------ |
| Значения для обоих `TaskInfo.url` и `TaskInfo.card` были указаны. | Значения для карты и URL-адреса были указаны. Разрешено одно или другое, но не то и другое. |
| Ни `TaskInfo.url` `TaskInfo.card` указанных, ни указанных. | Необходимо указать значение для карты или URL-адреса. |
| Недействительный `appId` . | Недействительный ID приложения. |
| Пользователь выбрал кнопку X, закрыв ее. | Пользователь отменил или закрыл модуль задач. |

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Пример вкладок модуля задач и ботов-V3 | Примеры для создания модулей задач. |[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a>Дополнительные ресурсы

[Вызов и закрытие модулей задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Использование модулей задач от ботов](~/task-modules-and-cards/task-modules/task-modules-bots.md)
