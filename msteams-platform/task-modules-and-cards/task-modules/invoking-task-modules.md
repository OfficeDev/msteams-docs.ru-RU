---
title: Вызов и закрытие модулей задач
description: 'В этой статье описаны: вызов и закрытие модулей задач, объект сведений о задаче, изменения размера модуля задач, синтаксис прямой ссылки модуля задач и приведены соответствующие примеры программного кода'
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: ae2eb0e1367feb5f1b31c47396277758e2385204
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111880"
---
# <a name="invoke-and-dismiss-task-modules"></a>Вызов и закрытие модулей задач

Модули задач можно вызывать из вкладок, ботов или по прямым ссылкам. Ответ может быть в формате HTML или JavaScript, либо в виде адаптивной карточки. Вызовы модулей задач и работа с ответом в виде взаимодействия пользователя допускают значительную гибкость. Механизм описан в следующей таблице.

| Вызывается с помощью | Модуль задач с HTML или JavaScript | Модуль задач с адаптивной карточкой |
| --- | --- | --- |
| JavaScript на вкладке | 1. Используйте функцию пакета SDK клиента Teams `tasks.startTask()` с необязательной функцией обратного вызова `submitHandler(err, result)`. <br/><br/> 2. В коде модуля задач, когда пользователь выполнил действия, вызовите функцию Teams SDK `tasks.submitTask()` с объектом `result` в качестве параметра. Если обратный вызов `submitHandler` указан в `tasks.startTask()`, Teams вызывает его с `result` в качестве параметра. Если при вызове `tasks.startTask()` произошла ошибка, вместо этого вызывается функция `submitHandler` со строкой `err`. <br/><br/> 3. Можно также указать значение `completionBotId` при вызове `teams.startTask()`. Тогда вместо этого боту отправляется `result`. | 1. Вызовите функцию пакета SDK клиента Teams `tasks.startTask()` с [объектом TaskInfo](#the-taskinfo-object) и `TaskInfo.card`, содержащим JSON для адаптивной карточки, показанной во всплывающем окне модуля задач. <br/><br/> 2. Если обратный вызов `submitHandler` указан в `tasks.startTask()`, Teams вызывает его со строкой `err` в качестве параметра в случае возникновения ошибки при вызове `tasks.startTask()` и в случае, когда пользователь закрывает всплывающее окно модуля задач нажатием X в правом верхнем углу. <br/><br/> 3. Если пользователь нажимает кнопку `Action.Submit`, ее объект `data` возвращается в качестве значения `result`. |
| Кнопка карточки бота | 1. Кнопки карточки бота в зависимости от типа кнопки могут вызывать модули задач двумя способами: по URL-адресу прямой ссылки или отправкой сообщения `task/fetch`. <br/><br/> 2. Если действием кнопки `type` является `task/fetch`, который представляет собой тип кнопки `Action.Submit` для адаптивных карточек, то боту отправляется событие `task/fetch invoke`, представляющее собой HTTP POST. Бот отвечает на запрос POST с HTTP 200 и телом ответа, содержащим оболочку вокруг [объекта TaskInfo](#the-taskinfo-object). Дополнительные сведения см. в статье о [вызове модуля задач с помощью `task/fetch`](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch). Teams показывает модуль задачи. <br/><br/> 3. После выполнения пользователем действий вызовите функцию Teams SDK `tasks.submitTask()` с объектом `result` в качестве параметра. Бот получает сообщение `task/submit invoke`, содержащее объект `result`. <br/><br/> 4. У вас есть три разных способа отреагировать на сообщение `task/submit`: не предпринимать никаких действий, если задание было успешно завершено, показать сообщение пользователю во всплывающем окне или вызвать другое окно модуля задач. Дополнительные сведения см. [в подробном обсуждении `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | <ul><li> Как и кнопки на карточках Bot Framework, кнопки на адаптивных карточках поддерживают два способа вызова модулей задач: `Action.openUrl` `task/fetch` `Action.Submit` URL-адреса прямых ссылок с кнопками и использование кнопок. </li></ul> <br/><br/> <ul><li> Модули задач с адаптивными карточками действуют аналогично сценарию с HTML или JavaScript. Основное различие заключается в том, что, поскольку при использовании адаптивных карточек JavaScript отсутствует, вызвать `tasks.submitTask()` невозможно. Вместо этого Teams получает объект `data` от `Action.Submit` и возвращает его в качестве полезных данных события `task/submit`. Дополнительные сведения см. в статье [о гибкости `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). </li></ul> |
| URL-адрес прямой ссылки <br/>[синтаксис URL-адреса](#task-module-deep-link-syntax) | 1. Teams вызывает модуль задачи, представляющий собой URL-адрес, фигурирующий внутри `<iframe>`, указанного в параметре `url` прямой ссылки. Обратный вызов `submitHandler` отсутствует. <br/><br/> 2. В JavaScript страницы в модуле задачи вызовите `tasks.submitTask()`, чтобы закрыть его с объектом `result` в качестве параметра, в точности как при вызове через кнопку карточки вкладки или бота. Однако логика завершения немного отличается. Если логика завершения находится на клиенте, то есть если бот отсутствует, обратного вызова `submitHandler` нет, поэтому любая логика завершения должна находиться в коде, предшествующем вызову `tasks.submitTask()`. Сообщения об ошибках вызова передаются только через консоль. Если у вас есть бот, можно указать параметр `completionBotId` в прямой ссылке для отправки объекта `result` через событие `task/submit`. | 1. Teams вызывает модуль задачи, представляющий собой тело карточки JSON адаптивной карточки, указанной в качестве значения параметра `card` прямой ссылки в кодировке URL. <br/><br/> 2. Пользователь закрывает модуль задачи, щелкнув значок X в правом верхнем углу модуля задач или нажав кнопку `Action.Submit` на карточке. Так как `submitHandler` отсутствует и не может быть вызван, у пользователя должен быть бот для отправки значения полей адаптивной карточки. Пользователь должен использовать параметр `completionBotId` в прямой ссылке, чтобы указать бота, которому будут отправлены данные с помощью события `task/submit invoke`. |

В следующем разделе описан объект `TaskInfo`, определяющий определенные атрибуты для модуля задачи.

## <a name="the-taskinfo-object"></a>Объект TaskInfo

Объект `TaskInfo` содержит метаданные для модуля задачи. Определите `url` для внедренного iFrame или `card` для адаптивной карточки. В следующей таблице приведено определение объекта:

| Атрибут | Тип | Описание |
| --- | --- | --- |
| `title` | string | Этот атрибут выводится под названием приложения, справа от его значка. |
| `height` | number или string | Этот атрибут может быть числом, представляющим высоту модуля задачи в пикселях, или `small`, `medium`или `large`. Дополнительные сведения см. в статье об [определении размера модулей задач](#task-module-sizing). |
| `width` | number или string | Этот атрибут может быть числом, представляющим ширину модуля задачи в пикселях, или `small`, `medium`или `large`. Дополнительные сведения см. в статье об [определении размера модулей задач](#task-module-sizing). |
| `url` | string | Этот атрибут представляет собой URL-адрес страницы, загруженной как `<iframe>` внутри модуля задач. Домен URL-адреса должен быть указан в массиве [validDomains array](~/resources/schema/manifest-schema.md#validdomains) в манифесте приложения. |
| `card` | Адаптивная карточка или вложение карточки бота адаптивной карточки | Этот атрибут представляет собой JSON для адаптивной карточки, которая показана в модуле задачи. Если пользователь производит вызов из бота, используйте JSON адаптивной карточки в объекте Bot Framework `attachment`. Если вызов производится из вкладки, пользователь должен использовать адаптивную карточку. Дополнительные сведения см. в разделе [Адаптивная карточка или вложение карточки бота адаптивной карточки](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | Этот атрибут открывает URL-адрес на вкладке браузера, если клиент не поддерживает функцию модуля задач. |
| `completionBotId` | string | Этот атрибут указывает идентификатор приложения бота для отправки результата взаимодействия пользователя с модулем задачи. Если этот параметр указан, бот получает событие `task/submit invoke` с объектом JSON в полезных данных события. |

> [!NOTE]
> Функция модуля задач требует, чтобы домены всех URL-адресов, которые вы хотите загрузить, были включены в массив `validDomains` в манифесте приложения.

В следующем разделе описана работа с размером модуля задач, что позволяет пользователю задать высоту и ширину модуля задачи.

## <a name="task-module-sizing"></a>Определение размера модуля задач

Используя целые значения `TaskInfo.width` и `TaskInfo.height`, задает высоту и ширину модуля задачи в пикселях. Однако в зависимости от размера окна команды и разрешения экрана они уменьшаются пропорционально, сохраняя пропорции ширины или высоты.

Если `TaskInfo.width` и `TaskInfo.height` представляют собой `"small"`, `"medium"`или `"large"`, размер красного прямоугольника на следующем изображении пропорционален размерам доступного пространства, а именно 20 %, 50 % и 60 % для `width` и 20 %, 50 % и 66 % для `height`:

:::image type="content" source="../../assets/images/task-module/task-module-example.png" alt-text="Пример модуля задач":::

Модули задач, вызываемые из вкладки, позволяют динамически изменить размер. После вызова `tasks.startTask()` можно вызвать `tasks.updateTask(newSize)`, где свойства высоты и ширины объекта newSize соответствуют спецификации TaskInfo, например `{ height: 'medium', width: 'medium' }`.

В следующем разделе приведены примеры внедрения модулей задач в видео с YouTube и в приложение PowerApp.

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>CSS модуля задач для модулей задач HTML или JavaScript

Модули задач на основе HTML или JavaScript имеют доступ ко всей области модуля задач под заголовком. Это обеспечивает большую гибкость, однако если вы хотите выравнивать заполнение по краям в соответствии с элементами заголовка и избегать ненужных полос прокрутки, пользователь должен предоставить правильный CSS. В следующих разделах приведены примеры для нескольких вариантов использования.

### <a name="example-1-youtube-video"></a>Пример 1. Видео с YouTube

YouTube предлагает возможность внедрять видео на веб-страницы. Внедрить видео на веб-страницах модуля задачи легко с помощью простой веб-страницы-заглушки.

:::image type="content" source="../../assets/images/task-module/youtube-example.png" alt-text="Пример с Youtube":::

Этот фрагмент программного кода представляет собой пример HTML-кода для веб-страницы без CSS:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  ⋮
</head>
<body>
  <div id="embed-container">
    <iframe width="1000" height="700" src="https://www.youtube.com/embed/rd0Rd8w3FZ0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>
  </div>
</body>
</html>
```

Этот фрагмент программного кода представляет собой пример CSS:

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 95%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

### <a name="example-2-powerapp"></a>Пример 2. PowerApp

Для внедрения PowerApp можно использовать тот же подход. Так как высота и ширина любого отдельного приложения PowerApp настраиваются, пользователь может изменить их для достижения нужного внешнего вида.

:::image type="content" source="../../assets/images/task-module/powerapp-example.png" alt-text="powerapp":::

Этот фрагмент представляет собой пример HTML-кода для PowerApp:

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

Этот фрагмент программного кода представляет собой пример CSS:

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 94%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

В следующем разделе приводятся сведения о вызове карточки с помощью адаптивной карточки или вложения карточки в бот адаптивной карточки.

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Адаптивная карточка или вложение карточки бота адаптивной карточки

В зависимости от способа вызова `card` необходимо использовать адаптивную карточку или вложение карточки бота адаптивной карточки, которая представляет собой адаптивную карточку, упакованную в объект вложения.

При вызове из вкладки пользователь должен использовать адаптивную карточку.

Этот фрагмент программного кода представляет собой пример кода адаптивной карточки.

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "text": "Here is a ninja cat:"
        },
        {
            "type": "Image",
            "url": "http://adaptivecards.io/content/cats/1.png",
            "size": "Medium"
        }
    ],
    "version": "1.0"
}
```

Этот фрагмент программного кода представляет собой пример вложения карточки в бот адаптивной карточки при вызове бота:

```json
{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
        "type": "AdaptiveCard",
        "body": [
            {
                "type": "TextBlock",
                "text": "Here is a ninja cat:"
            },
            {
                "type": "Image",
                "url": "http://adaptivecards.io/content/cats/1.png",
                "size": "Medium"
            }
        ],
        "version": "1.0"
    }
}
```

В следующем разделе приводятся сведения о синтаксисе прямой ссылки модуля задач, включая объект `TaskInfo` и `APP_ID` и `BOT_APP_ID`.

## <a name="task-module-deep-link-syntax"></a>Синтаксис прямой ссылки модуля задач

Прямая ссылка модуля задач — это сериализация объекта TaskInfo с двумя дополнительными параметрами, `APP_ID` и при необходимости `BOT_APP_ID`:

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Типы данных и допустимые значения для `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>` и `<TaskInfo.title>` см. в разделе об [объекте TaskInfo](#the-taskinfo-object).

> [!TIP]
> URL-адрес кодирует прямую ссылку при использовании параметра `card`, например [`encodeURI()`функцию](https://www.w3schools.com/jsref/jsref_encodeURI.asp) JavaScript.

В следующей таблице приведены сведения об `APP_ID` и `BOT_APP_ID`:

| Значение | Тип | Обязательный | Описание |
| --- | --- | --- | --- |
| `APP_ID` | string | Да | [Идентификатор приложения](~/resources/schema/manifest-schema.md#id), вызывающего модуль задачи. Массив [validDomains](~/resources/schema/manifest-schema.md#validdomains) в манифесте `APP_ID` должен содержать домен для `url`, если в URL-адресе присутствует `url`. Идентификатор приложения уже известен при вызове модуля задачи из вкладки или бота, поэтому он не включен в `TaskInfo`. |
| `BOT_APP_ID` | string | Нет | Если задано значение `completionBotId`, объект `result` отправляется с помощью сообщения `task/submit invoke` указанному боту. `BOT_APP_ID` должен быть указан как бот в манифесте приложения, то есть его нельзя отправить ни в один бот. |

> [!NOTE]
> `APP_ID` и `BOT_APP_ID` могут совпадать. Это происходит, когда у приложения есть рекомендованный бот для использования в качестве идентификатора приложения, при наличии такового.

В следующем разделе приводятся сведения об использовании клавиатуры с модулем задач приложения.

## <a name="keyboard-and-accessibility-guidelines"></a>Рекомендации по использованию клавиатуры и специальных возможностей

При работе с модулями задач на основе HTML или JavaScript вы должны обеспечить возможность использования модуля задач приложения с клавиатурой. Программы чтения с экрана также зависят от возможности навигации с помощью клавиатуры. Это включает следующие два момента:

* Использование [атрибута tabindex](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/tabindex) в тегах HTML для указания, каким элементам может быть передан фокус. Кроме того, используйте атрибут tabindex, чтобы определить, где он участвует в последовательной навигации с помощью клавиатуры, обычно с помощью клавиш <kbd>TAB</kbd> <kbd>и SHIFT-TAB</kbd>.
* Обработка нажатия клавиши <kbd>ESC</kbd> в JavaScript для модуля задачи. Этот фрагмент программного кода представляет собой пример обработки нажатия клавиши <kbd>ESC</kbd> :

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teams обеспечивает правильную работу навигации с помощью клавиатуры из заголовка модуля задач в HTML и наоборот.

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Пример модуля задач bots-V4 | Примеры для создания модулей задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|Примеры вкладок модуля задач и bots-V3 | Примеры для создания модулей задач. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Использование модулей задач во вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

## <a name="see-also"></a>См. также

* [Запрос разрешений устройства](~/concepts/device-capabilities/native-device-permissions.md)
* [Интеграция возможностей мультимедиа](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Интеграция функции сканирования QR-кода или штрихкода в Teams](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Интеграция функций местонахождения](~/concepts/device-capabilities/location-capability.md)
