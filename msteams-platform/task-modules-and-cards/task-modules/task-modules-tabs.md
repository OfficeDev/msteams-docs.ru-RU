---
title: Использование модулей задач на вкладках Microsoft Teams
description: В этой статье объясняется, как вызывать модули задач из вкладок Teams и отправлять их результаты с помощью клиентского пакета SDK Microsoft Teams. Включены примеры кода.
ms.localizationpriority: high
ms.topic: how-to
keywords: клиентский пакет SDK для вкладок Teams модулей задач
ms.openlocfilehash: eb199842a60832e6eb77575a7438cc9f52db6e09
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111229"
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

* Для параметра `TaskInfo.url` задано значение URL-адреса. Появляется окно модуля задач, и в нем загружается `TaskModule.url` как `<iframe>`. JavaScript на этой странице вызывает `microsoftTeams.initialize()`. Если на странице есть функция `submitHandler` и при вызове `microsoftTeams.tasks.startTask()` возникает ошибка, вызывается `submitHandler` с параметром `err`, которому присвоено значение строки ошибки с аналогичным содержанием. Дополнительные сведения см. в разделе [Ошибки при вызове модуля задач](#task-module-invocation-errors).
* Значением `taskInfo.card` является [JSON для адаптивной карточки](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). Отсутствует функция JavaScript `submitHandler` для вызова, когда пользователь закрывает адаптивную карточку или нажимает в ней кнопку. Единственный способ получить введенные пользователем данные — передать результат боту. Чтобы использовать модуль задач адаптивной карточки со вкладки, ваше приложение должно включать бота для получения любого отклика от пользователя.

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

`submitHandler` очень прост и передает значение `err` или `result` в консоль.

## <a name="submit-the-result-of-a-task-module"></a>Отправка результата модуля задач

Функция `submitHandler` находится на веб-странице `TaskInfo.url` и используется с `TaskInfo.url`. Если при вызове модуля задач возникает ошибка, немедленно вызывается ваша функция `submitHandler` со строкой `err`, указывающей, какая [ошибка произошла](#task-module-invocation-errors). Также вызывается функция `submitHandler` со строкой `err`, когда пользователь нажимает X в правом верхнем углу модуля задач, чтобы закрыть его.

Если ошибка вызова отсутствует и пользователь не нажимает X, чтобы закрыть ее, пользователь нажмет кнопку по завершении. В следующих разделах содержатся сведения о том, что происходит в зависимости от того, является ли это URL-адресом или адаптивной карточкой в модуле задач.

### <a name="html-or-javascript-taskinfourl"></a>`TaskInfo.url` HTML или JavaScript

После проверки входных данных пользователя вызовите функцию пакета SDK `microsoftTeams.tasks.submitTask()` под названием `submitTask()`. Вызовите `submitTask()` без параметров, если нужно, чтобы Teams просто закрыл модуль задач. Вы можете передать объект или строку в `submitHandler`.

Передайте результат в качестве первого параметра. Teams вызывает `submitHandler`, где `err` имеет значение `null`, а `result` — это объект или строка, переданные в `submitTask()`. Если вызвать `submitTask()` с параметром `result`, необходимо передать `appId` или массив строк `appId`. Это позволяет Teams убедиться, что приложение, отправляющее результат, совпадает с вызванным модулем задач.

### <a name="adaptive-card-taskinfocard"></a>`TaskInfo.card` адаптивной карточки

Когда вы вызываете модуль задач с помощью `submitHandler`, а пользователь нажимает кнопку `Action.Submit`, значения в карточке возвращаются в виде значения `result`. Если пользователь нажимает клавишу ESC или кнопку X в правом верхнем углу, вместо этого возвращается `err`. Если ваше приложение содержит бота в дополнение ко вкладке, вы можете просто включить `appId` бота в качестве значения `completionBotId` в объекте `TaskInfo`. Текст адаптивной карточки, заполненный пользователем, отправляется боту с помощью сообщения `task/submit invoke` при нажатии пользователем кнопки `Action.Submit`. Получаемая схема для объекта очень похожа на [схему, получаемую для сообщений task/fetch и task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). Единственным отличием является то, что схема объекта JSON является объектом адаптивной карточки, а не объектом, содержащим объект адаптивной карточки, как [при использовании адаптивных карточек с ботами](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

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
|Примеры вкладок модуля задач и bots-V3 | Примеры для создания модулей задач. |[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Использование модулей задач из ботов](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>Дополнительные ресурсы

[Вызов и закрытие модулей задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
