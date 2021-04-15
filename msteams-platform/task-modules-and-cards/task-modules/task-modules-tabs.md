---
title: Использование модулей задач на вкладке Microsoft Teams
description: Объясняет, как вызывать модули задач из вкладок Teams с помощью SDK клиента Microsoft Teams.
ms.topic: how-to
keywords: модули задач группы вкладок sdk клиента
ms.openlocfilehash: dbcc6ce0ba31bae43335334dfb1c354acc33a2a0
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696033"
---
# <a name="using-task-modules-in-tabs"></a>Использование модулей задач во вкладках

Добавление модуля задач на вкладку может значительно упростить работу пользователя для любых процессов, которые требуют ввода данных. Модули задач позволяют собирать входные данные в всплывающее окантовка Teams. Хорошим примером этого является редактирование карт Планировщика; вы можете использовать модули задач для создания аналогичного опыта.

Для поддержки функции модуля задач в [клиентскую SDK Microsoft Teams](/javascript/api/overview/msteams-client)добавлены две новые функции:

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

Давайте посмотрим, как каждый из них работает.

## <a name="invoking-a-task-module-from-a-tab"></a>Ссылки на модуль задач со вкладки

Чтобы вызвать модуль задач со вкладки, используйте передачу объекта `microsoftTeams.tasks.startTask()` [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) и необязательный вызов `submitHandler` функции. Как было описано выше, необходимо рассмотреть два случая:

1. Значение `TaskInfo.url` установлено для URL-адреса. Окно модуля задач отображается и `TaskModule.url` загружается как `<iframe>` внутреннее. JavaScript на этой странице должен вызвать `microsoftTeams.initialize()` . Если на странице есть функция и при вызове есть ошибка, то вызывается с набором к строке ошибки, указывающей ошибку, как описано `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` [ниже.](#task-module-invocation-errors)
1. Значение `taskInfo.card` JSON для [адаптивной карты](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). В этом случае не нужно вызывать функцию JavaScript, когда пользователь закрывает или нажимает кнопку на адаптивной карте; единственный способ получить то, что вошел пользователь, это передача результата `submitHandler` боту. Чтобы использовать модуль задач адаптивной карты со вкладки, приложение должно включить бот, чтобы получить любую информацию от пользователя. Это объясняется ниже.

## <a name="example-invoking-a-task-module"></a>Пример: наводка модуля задач

Ниже приведен код, адаптированный из [примера модуля задач.](~/task-modules-and-cards/what-are-task-modules.md#code-sample) Вот как выглядит модуль задач:

![Модуль задач — настраиваемая форма](~/assets/images/task-module/task-module-custom-form.png)

Это `submitHandler` очень просто; оно просто перекликается со значением консоли или `err` `result` консоли:

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

## <a name="submitting-the-result-of-a-task-module"></a>Отправка результатов модуля задач

Функция `submitHandler` используется с `TaskInfo.url` . Функция `submitHandler` находится на `TaskInfo.url` веб-странице. Если при вызове модуля задачи возникла ошибка, функция будет немедленно вызвана строкой, указывающей, какая `submitHandler` `err` ошибка [произошла.](#task-module-invocation-errors) Функция также называется строкой, когда пользователь нажимает X в правом верхнем `submitHandler` `err` справа от модуля задач.

Если нет ошибки вызова и пользователь не нажимает X, чтобы отклонять ее, пользователь нажимает кнопку по завершению. В зависимости от того, url-адрес или адаптивная карта в модуле задач, вот что происходит:

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript ( `TaskInfo.url` )

После проверки того, что вошел пользователь, вызовите функцию SDK (далее она называется для целей `microsoftTeams.tasks.submitTask()` `submitTask()` читаемости). Вы можете звонить без параметров, если вы просто хотите, чтобы Teams закрыли модуль задач, но большую часть времени вы хотите передать объект или строку `submitTask()` в `submitHandler` ваш .

Передай результат в качестве первого параметра. Команды будут `submitHandler` вызывать, `err` где будет и будет объект или `null` `result` строка, которую вы передали `submitTask()` . Если вы вызываете с параметром, необходимо передать или массив строк: это позволяет Teams проверить, что приложение, отправляя результат, является тем же, что вызывалось в модуль `submitTask()` `result`  `appId` `appId` задач.

### <a name="adaptive-card-taskinfocard"></a>Адаптивная карта ( `TaskInfo.card` )

Если вы вызывали модуль задач с кнопкой , когда пользователь нажимает кнопку, значения в карточке будут возвращены в качестве `submitHandler` `Action.Submit` значения `result` . Если пользователь нажал кнопку Esc или нажал клавишу X, он будет `err` возвращен. Кроме того, если приложение содержит бот в дополнение к вкладке, вы можете просто включить бот в качестве значения `appId` `completionBotId` в `TaskInfo` объекте. При нажатии кнопки в бот будет отправлено тело адаптивной карты (как заполнено `task/submit invoke` `Action.Submit` пользователем). Схема объекта, который вы получаете, очень похожа на схему, которую вы получаете для задач/извлечений и [задач/отправки сообщений;](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages) Единственное отличие состоит в том, что схема объекта JSON является объектом  адаптивной карты, а не объектом, содержащим объект адаптивной карты, как когда адаптивные карты используются с [ботами.](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)

## <a name="example-submitting-the-result-of-a-task-module"></a>Пример: отправка результата модуля задач

Отзыв формы [в модуле задач выше](#example-invoking-a-task-module) с помощью HTML-формы. Вот где определена форма:

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

В этой форме есть пять полей, но нам интересны только значения трех из них для этого примера: `name` `email` и `favoriteBook` .

Вот `validateForm()` функция, которая `submitTask()` вызывает:

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

## <a name="task-module-invocation-errors"></a>Ошибки при вызове модуля задач

Вот возможные значения, `err` которые могут быть получены `submitHandler` вашим:

| Проблема | Сообщение об ошибке (значение `err` ) |
| ------- | ------------------------------ |
| Значения для обоих `TaskInfo.url` и `TaskInfo.card` были указаны. | "Значения для карты и URL-адреса были указаны. Разрешено одно или другое, но не то и другое". |
| Ни `TaskInfo.url` `TaskInfo.card` указанных, ни указанных. | "Необходимо указать значение для карты или URL-адреса". |
| Недействительный `appId` . | "Недействительный appId". |
| Пользователь нажал кнопку X, закрыв ее. | "Пользователь отменил или закрыл модуль задач". |
