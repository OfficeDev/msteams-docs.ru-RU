---
title: Использование модулей задач в Microsoft Teams вкладками
description: Объясняет, как вызывать модули задач с Teams вкладок и отправку результатов с помощью Microsoft Teams клиентской SDK. Он включает в себя примеры кода.
ms.localizationpriority: medium
ms.topic: how-to
keywords: модули задач группы вкладок sdk клиента
ms.openlocfilehash: 43b58a4f8ec1176c2d931f130a33c6610a078187
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453644"
---
# <a name="use-task-modules-in-tabs"></a>Использование модулей задач во вкладках

Добавьте модуль задач на вкладку, чтобы упростить работу пользователя для любых процессов, которые требуют ввода данных. Модули задач позволяют собирать входные данные в всплывающее Teams-Aware Microsoft. Хорошим примером этого является редактирование карт Планировщика. Для создания аналогичного опыта можно использовать модули задач.

Для поддержки функции модуля задач в [SDK клиента Teams две новые функции](/javascript/api/overview/msteams-client). В следующем коде показан пример этих двух функций:

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

Чтобы вызвать модуль задач со вкладки, используйте `microsoftTeams.tasks.startTask()` передачу объекта [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) и необязательный `submitHandler` вызов функции. Необходимо рассмотреть два случая:

* Значение установлено `TaskInfo.url` для URL-адреса. Окно модуля задач отображается `TaskModule.url` и загружается как внутреннее `<iframe>` . JavaScript на этой странице вызывает `microsoftTeams.initialize()`. Если на странице есть `submitHandler` `microsoftTeams.tasks.startTask()`функция и ошибка при вызове, `submitHandler` `err` то вызывается с задаваемой строкой ошибки, указывающей то же самое. Дополнительные сведения см. [в ссылке на ошибки вызовов модулей задач](#task-module-invocation-errors).
* Значение JSON `taskInfo.card` для [адаптивной карты](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). Функция JavaScript `submitHandler` не может вызываться при закрытии или нажатии кнопки на адаптивной карте. Единственный способ получить то, что вошел пользователь, — это передача результата боту. Чтобы использовать модуль задач адаптивной карты со вкладки, приложение должно включить бот, чтобы получить любой ответ от пользователя.

В следующем разделе приводится пример ссылки на модуль задач.

## <a name="example-of-invoking-a-task-module"></a>Пример ссылки на модуль задач

На следующем изображении отображается модуль задач:

![Модуль задач — настраиваемая форма](~/assets/images/task-module/task-module-custom-form.png)

Следующий код адаптируется из [примера модуля задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample):

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

Это `submitHandler` очень просто, и оно повторяет значение консоли `err` или `result` консоли.

## <a name="submit-the-result-of-a-task-module"></a>Отправка результатов модуля задач

Функция `submitHandler` находится на веб-странице `TaskInfo.url` и используется с `TaskInfo.url`. Если при вызове модуля задач возникла ошибка, `submitHandler` `err` функция немедленно вызывается строкой, указывающей, какая [ошибка произошла](#task-module-invocation-errors). Функция `submitHandler` также называется строкой `err` , когда пользователь выбирает X в правом верхнем справа от модуля задач, чтобы закрыть ее.

Если ошибки вызова нет и пользователь не выбирает X, чтобы отклонять ее, пользователь выбирает кнопку по завершению. В зависимости от url-адреса или адаптивной карты в модуле задач в следующих разделах указаны сведения о том, что происходит.

### <a name="html-or-javascript-taskinfourl"></a>HTML или JavaScript `TaskInfo.url`

После проверки входных данных пользователя вызываем `microsoftTeams.tasks.submitTask()` функцию SDK, которая называется `submitTask()`. Вызов `submitTask()` без параметров, если Teams закрыть модуль задач. Вы можете передать объект или строку в ваш `submitHandler`.

Передай результат в качестве первого параметра. Teams вызывает`submitHandler`, где находится `null` `result` и является объект или строка, которую вы передали `submitTask()``err` . Если вы звоните `submitTask()` с параметром `result` , необходимо передать `appId` или массив строк `appId` . Это позволяет Teams, чтобы проверить, что приложение, отправляя результат, является таким же, как вызываемого модуля задач.

### <a name="adaptive-card-taskinfocard"></a>Адаптивная карта `TaskInfo.card`

Когда вы вызываете модуль задач `submitHandler` `Action.Submit` с помощью кнопки, а пользователь выбирает кнопку, значения в карточке возвращаются в качестве значения `result`. Если пользователь выбирает ключ Esc или X в правом верхнем справа, `err` возвращается вместо него. Если приложение содержит бот в дополнение к вкладке, `appId` `completionBotId` вы можете просто включить бот в качестве значения в объекте `TaskInfo` . Тело адаптивной карты `task/submit invoke` , заполненное пользователем, отправляется боту с помощью сообщения, когда пользователь выбирает кнопку `Action.Submit` . Схема объекта, который вы получаете, очень похожа на схему, которую вы получаете для задач и задач и [отправки сообщений](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). Единственное отличие состоит в том, что схема объекта JSON является объектом Адаптивной карты, а не объектом, содержащим объект адаптивной карты, как при использования адаптивных карт с [ботами](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

В следующем разделе приводится пример отправки результатов модуля задач.

## <a name="example-of-submitting-the-result-of-a-task-module"></a>Пример отправки результата модуля задач

Дополнительные сведения см. в [htmL-форме в модуле задач](#example-of-invoking-a-task-module). В следующем коде приводится пример определения формы:

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Существует пять полей в этой форме, но для этого примера требуется только три значения, `name`и `email``favoriteBook`.

В следующем коде приводится пример функции `validateForm()` , которая вызывает `submitTask()`:

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

В следующей таблице возможен доступ `err` `submitHandler`к следующим значениям:

| Проблема | Сообщение об ошибке, значение `err` |
| ------- | ------------------------------ |
| Значения для обоих и `TaskInfo.url` были `TaskInfo.card` указаны. | Значения для карты и URL-адреса были указаны. Разрешено одно или другое, но не то и другое. |
| Ни указанных `TaskInfo.url` , ни `TaskInfo.card` указанных. | Необходимо указать значение для карты или URL-адреса. |
| Недействительный `appId`. | Недействительный ID приложения. |
| Пользователь выбрал кнопку X, закрыв ее. | Пользователь отменил или закрыл модуль задач. |

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Пример вкладок модуля задач и ботов-V3 | Примеры для создания модулей задач. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Использование модулей задач от ботов](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>См. также

[Вызов и закрытие модулей задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
