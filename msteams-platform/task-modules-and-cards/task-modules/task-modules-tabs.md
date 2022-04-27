---
title: Использование модулей задач на Microsoft Teams вкладок
description: В этой статье объясняется, как вызывать модули задач Teams вкладок и отправлять результаты с помощью Microsoft Teams клиентского пакета SDK. Он включает примеры кода.
ms.localizationpriority: medium
ms.topic: how-to
keywords: пакет SDK клиента для вкладок teams для модулей задач
ms.openlocfilehash: 63ac1df5b9cdbbba46ba204103a9a5c989b3a323
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073761"
---
# <a name="use-task-modules-in-tabs"></a>Использование модулей задач во вкладках

Добавьте модуль задач на вкладку, чтобы упростить взаимодействие с пользователем для любых рабочих процессов, для которых требуется ввод данных. Модули задач позволяют собирать входные данные во всплывающем Teams-Aware Microsoft. Хорошим примером этого является редактирование карт Планировщика. Для создания аналогичного интерфейса можно использовать модули задач.

Для поддержки функции модуля задач в клиентский пакет [SDK](/javascript/api/overview/msteams-client) Teams две новые функции. В следующем коде показан пример этих двух функций:

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

Вы можете увидеть, как выполняется вызов модуля задачи на вкладке и отправка результата модуля задачи.

## <a name="invoke-a-task-module-from-a-tab"></a>Вызов модуля задачи на вкладке

Чтобы вызвать модуль задачи с вкладки, `microsoftTeams.tasks.startTask()` используйте передачу объекта [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) и необязательной `submitHandler` функции обратного вызова. Существует два варианта, которые следует учитывать:

* Для параметра `TaskInfo.url`  задано значение URL-адреса. Появится окно модуля задач, и `TaskModule.url` оно будет загружено как `<iframe>` внутреннее. Вызовы JavaScript на этой странице `microsoftTeams.initialize()`. Если на странице есть `submitHandler` `microsoftTeams.tasks.startTask()`функция и при вызове возникает ошибка, `submitHandler` `err` вызывается с задаваемой строкой ошибки, указывающая на то же самое. Дополнительные сведения см. [в разделе об ошибках вызова модуля задач](#task-module-invocation-errors).
* Значением является `taskInfo.card` [JSON для адаптивной карточки](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). Функция JavaScript `submitHandler` , вызываемая при закрытии или нажатии кнопки на адаптивной карточке, отсутствует. Единственный способ получить введенные пользователем данные — передать результат боту. Чтобы использовать модуль задачи адаптивной карточки на вкладке, приложение должно включать бота, чтобы получить любой ответ от пользователя.

В следующем разделе приведен пример вызова модуля задачи.

## <a name="example-of-invoking-a-task-module"></a>Пример вызова модуля задачи

На следующем рисунке показан модуль задачи:

:::image type="content" source="../../assets/images/task-module/task-module-custom-form.png" alt-text="Настраиваемая форма модуля задач":::

Следующий код адаптирован из примера [модуля задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample):

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

Это `submitHandler` очень просто, и оно выводит значение или `err` в `result` консоль.

## <a name="submit-the-result-of-a-task-module"></a>Отправка результата модуля задачи

Функция `submitHandler` находится на веб-странице `TaskInfo.url` и используется с `TaskInfo.url`. Если при вызове модуля задачи возникает ошибка, `submitHandler` `err` функция немедленно вызывается со строкой, указывающая, какая [ошибка произошла](#task-module-invocation-errors). Функция `submitHandler` также вызывается со строкой `err` , когда пользователь выбирает X в правом верхнем углу модуля задачи, чтобы закрыть ее.

Если ошибка вызова отсутствует и пользователь не выбирает X, чтобы закрыть ее, пользователь нажмет кнопку по завершении. В зависимости от того, является ли это URL-адрес или адаптивная карточка в модуле задачи, в следующих разделах содержатся сведения о том, что происходит.

### <a name="html-or-javascript-taskinfourl"></a>HTML или JavaScript `TaskInfo.url`

После проверки входных данных пользователя вызовите функцию пакета SDK, `microsoftTeams.tasks.submitTask()` называемую `submitTask()`.NET. Вызов `submitTask()` без параметров, если Teams закрыть модуль задачи. Вы можете передать объект или строку в файл `submitHandler`.

Передайте результат в качестве первого параметра. Teams вызывает`submitHandler`, где находится `null` `result` и является объект или строка, которые вы передали`submitTask()``err`. При вызове `submitTask()` с параметром `result` необходимо передать массив `appId` строк `appId` или массив. Это позволяет Teams убедиться, что приложение, отправляющее результат, совпадает с вызываемого модуля задачи.

### <a name="adaptive-card-taskinfocard"></a>Адаптивная карточка `TaskInfo.card`

При вызове модуля задач с помощью кнопки `submitHandler` `Action.Submit` , когда пользователь нажмет кнопку, значения в карточке возвращаются в виде значения `result`. Если пользователь выбирает клавишу ESC или X в правом верхнем углу, `err` возвращается вместо него. Если приложение содержит бот в дополнение к вкладке, `appId` `completionBotId` вы можете просто включить бот в качестве значения объекта `TaskInfo` . Текст адаптивной карточки `task/submit invoke` , заполненный пользователем, отправляется боту с помощью сообщения, когда пользователь нажмет кнопку `Action.Submit` . Схема получаемый объект очень похожа на схему, получаемую для сообщений [задачи, получения и отправки](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). Единственным отличием является то, что схема объекта JSON является объектом адаптивной карточки, а не объектом, содержащим объект адаптивной карточки, как при использовании адаптивных карточек [с ботами](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

В следующем разделе приведен пример отправки результата модуля задачи.

## <a name="example-of-submitting-the-result-of-a-task-module"></a>Пример отправки результата модуля задачи

Дополнительные сведения см. в [HTML-форме в модуле задачи](#example-of-invoking-a-task-module). В следующем коде приведен пример определения формы:

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

В этой форме есть пять полей, но в этом примере требуются только три значения: `name``email`и `favoriteBook`.

В следующем коде приведен пример функции`validateForm()`, которая вызывает:`submitTask()`

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

Следующий раздел содержит сведения о проблемах вызова модуля задач и их сообщениях об ошибках.

## <a name="task-module-invocation-errors"></a>Ошибки при вызове модуля задач

В следующей таблице приведены возможные значения `err` , которые могут быть получены вашими `submitHandler`:

| Проблема | Сообщение об ошибке со значением `err` |
| ------- | ------------------------------ |
| Значения для обоих значений `TaskInfo.url` и `TaskInfo.card` были указаны. | Были указаны значения для карточки и URL-адреса. Одно или другое, но не оба, разрешено. |
| Не указано `TaskInfo.url` и не `TaskInfo.card` указано. | Необходимо указать значение для карточки или URL-адреса. |
| Недопустимая `appId`. | Недопустимый идентификатор приложения. |
| Пользователь нажмет кнопку X и закроет ее. | Пользователь отменил или закрыл модуль задачи. |

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Примеры вкладок модуля задач и bots-V3 | Примеры для создания модулей задач. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Использование модулей задач от ботов](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>См. также

[Вызов и закрытие модулей задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
