---
title: Использование модулей задач на вкладках Microsoft Teams
description: Узнайте, как вызывать модули задач Teams вкладок и отправлять результаты с помощью Microsoft Teams клиентского пакета SDK. Включены примеры кода.
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: a55ea89e67bf70254d52791d1ed5f0a1c573e89e
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142068"
---
# <a name="use-task-modules-in-tabs"></a>Использование модулей задач во вкладках

Добавьте модуль задач на вкладку, чтобы упростить взаимодействие с пользователем в любых рабочих процессах, для которых требуется ввод данных. Модули задач позволяют собирать входные данные во всплывающем окне в контексте Microsoft Teams. Хорошим примером этого является редактирование карточек Планировщика. Для создания аналогичного интерфейса вы можете использовать модули задач.

Для поддержки функции модуля задач в [клиентский пакет SDK Teams](/javascript/api/overview/msteams-client) добавлены две новые функции. В следующем коде показан пример этих двух функций.

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

Вы можете увидеть, как выполняется вызов модуля задачи со вкладки, а результат отправляется в модуль задач.

## <a name="invoke-a-task-module-from-a-tab"></a>Вызов модуля задач со вкладки

Чтобы вызвать модуль задачи со вкладки, используйте команду `microsoftTeams.tasks.startTask()`, передающую объект [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object), и необязательную функцию обратного вызова `submitHandler`. Необходимо рассмотреть два случая.

* Для параметра `TaskInfo.url` задано значение URL-адреса. Появляется окно модуля задач, и в нем загружается `TaskModule.url` как `<iframe>`. JavaScript на этой странице вызывает `microsoftTeams.initialize()`. Если на странице есть `submitHandler` `microsoftTeams.tasks.startTask()`функция и при вызове возникает ошибка, `submitHandler` `err` вызывается с задаваемой строкой ошибки, указывающая на то же самое. Дополнительные сведения см. в разделе [Ошибки при вызове модуля задач](#task-module-invocation-errors).
* Значением `taskInfo.card` является [JSON для адаптивной карточки](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). Функция JavaScript `submitHandler` , вызываемая при закрытии или нажатии кнопки на адаптивной карточке, отсутствует. Единственный способ получить введенные пользователем данные — передать результат боту. Чтобы использовать модуль задач адаптивной карточки со вкладки, ваше приложение должно включать бота для получения любого отклика от пользователя.

В следующем разделе приведен пример вызова модуля задач.

## <a name="example-of-invoking-a-task-module"></a>Пример вызова модуля задач

На следующем изображении показан модуль задач.

:::image type="content" source="../../assets/images/task-module/task-module-custom-form.png" alt-text="Настраиваемая форма модуля задач":::

Следующий код адаптирован из примера [модуля задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample).

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

Это `submitHandler` просто, и оно выводит значение или `err` возвращается `result` в консоль.

## <a name="submit-the-result-of-a-task-module"></a>Отправка результата модуля задач

Функция `submitHandler` находится на веб-странице `TaskInfo.url` и используется с `TaskInfo.url`. Если при вызове модуля задачи возникает ошибка, `submitHandler` `err` функция немедленно вызывается со строкой, указывающая, какая [ошибка произошла](#task-module-invocation-errors). Также вызывается функция `submitHandler` со строкой `err`, когда пользователь нажимает X в правом верхнем углу модуля задач, чтобы закрыть его.

Если ошибка вызова отсутствует и пользователь не выбирает X, чтобы закрыть ее, пользователь нажмет кнопку по завершении. В зависимости от того, является ли это URL-адрес или адаптивная карточка в модуле задачи, в следующих разделах приводятся сведения о том, что происходит.

### <a name="html-or-javascript-taskinfourl"></a>`TaskInfo.url` HTML или JavaScript

После проверки входных данных пользователя вызовите функцию пакета SDK `microsoftTeams.tasks.submitTask()` под названием `submitTask()`. Вызовите `submitTask()` без параметров, если нужно, чтобы Teams просто закрыл модуль задач. Вы можете передать объект или строку в `submitHandler`.

Передайте результат в качестве первого параметра. Teams вызывает `submitHandler`, где `err` имеет значение `null`, а `result` — это объект или строка, переданные в `submitTask()`. Если вызвать `submitTask()` с параметром `result`, необходимо передать `appId` или массив строк `appId`. Это позволяет Teams убедиться, что приложение, отправляющее результат, совпадает с вызванным модулем задач.

### <a name="adaptive-card-taskinfocard"></a>`TaskInfo.card` адаптивной карточки

Когда вы вызываете модуль задач с помощью `submitHandler`, а пользователь нажимает кнопку `Action.Submit`, значения в карточке возвращаются в виде значения `result`. Если пользователь нажимает клавишу ESC или кнопку X в правом верхнем углу, вместо этого возвращается `err`. Если приложение содержит бот в дополнение к вкладке, `appId` `completionBotId` вы можете включить бот в качестве значения объекта `TaskInfo` . Текст адаптивной карточки, заполненный пользователем, отправляется боту с помощью сообщения `task/submit invoke` при нажатии пользователем кнопки `Action.Submit`. Схема получаемый объект аналогична схеме, получаемой для сообщений [задачи, получения и отправки](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). Единственным отличием является то, что схема объекта JSON является объектом адаптивной карточки, а не объектом, содержащим объект адаптивной карточки, как [при использовании адаптивных карточек с ботами](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

В следующем разделе приведен пример отправки результата модуля задач.

## <a name="example-of-submitting-the-result-of-a-task-module"></a>Пример отправки результата модуля задач

Дополнительные сведения см. в разделе [HTML-форма в модуле задач](#example-of-invoking-a-task-module). В следующем коде приведен пример места определения формы.

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

В этой форме есть пять полей, но в этом примере требуются только три значения: `name`, `email` и `favoriteBook`.

В следующем коде приведен пример функции `validateForm()`, которая вызывает `submitTask()`.

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

В следующем разделе указаны проблемы при вызове модуля задач и соответствующие сообщения об ошибках.

## <a name="task-module-invocation-errors"></a>Ошибки при вызове модуля задач

В следующей таблице приведены возможные значения `err`, которые могут быть получены вашим `submitHandler`.

| Проблема | Сообщение об ошибке, которое является значением `err` |
| ------- | ------------------------------ |
| Указаны значения как для `TaskInfo.url`, так и для `TaskInfo.card`. | Указаны значения для карточки и URL-адреса. Допустимо лишь одно значение (не оба). |
| Не указаны `TaskInfo.url` и `TaskInfo.card`. | Необходимо указать значение для карточки или URL-адреса. |
| Недопустимый `appId`. | Недопустимый идентификатор приложения. |
| Пользователь нажал кнопку X для закрытия. | Пользователь отменил или закрыл модуль задач. |

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Примеры вкладок модуля задач и bots-V3 | Примеры для создания модулей задач. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Использование модулей задач из ботов](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>Дополнительные ресурсы

[Вызов и закрытие модулей задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
