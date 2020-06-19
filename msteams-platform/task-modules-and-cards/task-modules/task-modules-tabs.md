---
title: Использование модулей задач на вкладках Microsoft Teams
description: Сведения о том, как вызывать модули задач из вкладок Teams с помощью клиентского пакета SDK Microsoft Teams.
keywords: модули задач вкладки Teams клиентский пакет SDK
ms.openlocfilehash: e10958195713f338a9b5e0a0672d8b6a29da9264
ms.sourcegitcommit: 2a84a3c8b10771e37ce51bf603a967633947a3e4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/10/2020
ms.locfileid: "44801200"
---
# <a name="using-task-modules-in-tabs"></a>Использование модулей задач на вкладках

Добавление модуля задач на вкладку может значительно упростить взаимодействие пользователя с рабочими процессами, требующими ввода данных. Модули задач позволяют собирать свои данные в всплывающем окне, поддерживающем Teams. Хорошим примером является редактирование карточек планировщика; для создания аналогичных возможностей можно использовать модули задач.

Для поддержки функции модуля задач в [клиентский пакет SDK Microsoft Teams](/javascript/api/overview/msteams-client)добавлены две новые функции:

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

Давайте посмотрим, как работает каждый из них.

## <a name="invoking-a-task-module-from-a-tab"></a>Вызов модуля задачи из вкладки

Чтобы вызвать модуль задач на вкладке, используйте `microsoftTeams.tasks.startTask()` передачу [объекта таскинфо](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) и необязательную `submitHandler` функцию обратного вызова. Как было сказано ранее, следует учитывать два случая:

1. Значение равно `TaskInfo.url` URL-адресу. Откроется окно модуль задачи, в котором `TaskModule.url` она загружена `<iframe>` . На этой странице должен вызываться JavaScript `microsoftTeams.initialize()` . Если `submitHandler` на странице имеется функция и возникает ошибка при вызове `microsoftTeams.tasks.startTask()` , `submitHandler` вызывается параметр WITH `err` Set to String Error, указывающий на ошибку, как описано [ниже](#task-module-invocation-errors).
1. Значение `taskInfo.card` — это [Формат JSON для адаптивной карточки](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). В этом случае, очевидно, не существует функции JavaScript, `submitHandler` которая вызывается, когда пользователь закрывает или нажимает кнопку на адаптивной карточке; единственный способ получить значение, введенное пользователем, — передать результат в Bot. Чтобы использовать модуль задачи адаптивной карточки на вкладке, ваше приложение должно включать Bot для получения информации от пользователя. Это объясняется ниже.

## <a name="example-invoking-a-task-module"></a>Пример: вызов модуля задачи

Приведенный ниже код передается из [примера модуля задач](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples). Вот как выглядит модуль задачи:

![Модуль задачи — настраиваемая форма](~/assets/images/task-module/task-module-custom-form.png)

Это `submitHandler` очень простая программа, которая просто отображает значение `err` или `result` в консоли:

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

## <a name="submitting-the-result-of-a-task-module"></a>Отправка результата модуля задачи

`submitHandler`Функция используется с `TaskInfo.url` . `submitHandler`Функция находится на `TaskInfo.url` веб-странице. При возникновении ошибки при вызове модуля задач `submitHandler` функция будет сразу же вызываться со `err` строкой, указывающей, какая [Ошибка возникла](#task-module-invocation-errors). `submitHandler`Функция также вызывается с помощью `err` строки, когда пользователь нажимает клавишу X в верхнем правом углу модуля задач.

Если нет ошибки вызова, а пользователь не нажмет клавишу X, то при завершении работы пользователь нажимает кнопку. В зависимости от того, является ли URL-адрес или Адаптивная карта в модуле задач, происходит следующее:

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript ( `TaskInfo.url` )

После проверки того, что ввел пользователь, вы вызываете `microsoftTeams.tasks.submitTask()` функцию SDK (которая называется "в дальнейшем `submitTask()` " для удобства чтения). Вы можете вызвать `submitTask()` без параметров, если вы хотите, чтобы команда закрывала модуль задач, но в большинстве случаев требуется передать объект или строку в `submitHandler` .

Передайте результат в качестве первого параметра. Teams вызовет, `submitHandler` где `err` будет использоваться `null` `result` объект или строка, которые вы передали `submitTask()` . При вызове `submitTask()` с `result` параметром **необходимо** передать объект `appId` или массив `appId` строк: Это позволяет Teams проверить, что приложение отправляет результат, то же, что вызвало модуль задачи.

### <a name="adaptive-card-taskinfocard"></a>Адаптивная карта ( `TaskInfo.card` )

Если вы вызвали модуль Task с параметром `submitHandler` , когда пользователь нажимает кнопку, `Action.Submit` значения в карточке будут возвращены как значение `result` . Если пользователь нажимает кнопку ESC или нажимает клавишу X, `err` возвращается вместо него. Кроме того, если ваше приложение содержит Bot в дополнение к вкладке, можно просто включить `appId` объект Bot в качестве значения `completionBotId` в `TaskInfo` объект. Текст адаптивной карточки (которая заполняется пользователем) будет отправлен в объект Bot через `task/submit invoke` сообщение, когда пользователь нажимает `Action.Submit` кнопку. Схема получаемого объекта очень похожа на [схему, полученную для сообщений Task/Receive и Task/отправить](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). Единственное отличие состоит в том, что схема объекта JSON является объектом адаптивной карточки, а не объектом, *содержащим* объект адаптивной карточки, как [при использовании адаптивных карточек с Боты](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

## <a name="example-submitting-the-result-of-a-task-module"></a>Пример: отправка результата модуля задачи

Подпомните [форму в модуле задач выше](#example-invoking-a-task-module) с HTML-формой. Ниже показано, где определяется форма:

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

В этой форме имеется пять полей, но для этого примера требуются только значения трех из них: `name` , `email` и `favoriteBook` .

Вот `validateForm()` функция, которая вызывает `submitTask()` :

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

## <a name="task-module-invocation-errors"></a>Ошибки вызовов модулей задач

Ниже приведены возможные значения `err` , которые могут быть получены `submitHandler` :

| Проблема | Сообщение об ошибке (значение `err` ) |
| ------- | ------------------------------ |
| Указаны значения для обоих типов `TaskInfo.url` `TaskInfo.card` . | "Указаны значения для карты и URL-адреса. Разрешены только один или другой, но не оба. " |
| Ни `TaskInfo.url` значение `TaskInfo.card` , ни не указано. | "Необходимо указать значение для каждой из карточек или URL-адреса". |
| Недопустимый `appId` . | "Недопустимый appId." |
| Нажатая пользователем кнопка X, закрывающая ее. | "Пользователь отменил/закрыл модуль задач". |
