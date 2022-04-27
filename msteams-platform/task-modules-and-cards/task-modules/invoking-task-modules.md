---
title: Вызов и закрытие модулей задач
description: Сведения о вызове и закрытии модулей задач, объекте сведений о задаче, изменениях размера модуля задач, синтаксисе глубокой ссылки модуля задач с помощью примеров кода
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 5685e789dd6f4ad7cc39173e11af15dd9f7360fe
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073697"
---
# <a name="invoke-and-dismiss-task-modules"></a>Вызов и закрытие модулей задач

Модули задач можно вызывать из вкладок, ботов или прямых ссылок. Ответ может быть либо в ФОРМАТЕ HTML, JavaScript, либо в виде адаптивной карточки. Существует много гибкости с точки зрения того, как вызываются модули задач и как работать с ответом на взаимодействие пользователя. В следующей таблице описано, как это работает.

| Вызывается с помощью | Модуль задач с HTML или JavaScript | Модуль задач с адаптивной карточкой |
| --- | --- | --- |
| JavaScript на вкладке | 1. Используйте функцию Teams клиентского пакета SDK `tasks.startTask()` с необязательной `submitHandler(err, result)` функцией обратного вызова. <br/><br/> 2. В коде модуля задач, когда пользователь выполнил действия, вызовите функцию Teams SDK `tasks.submitTask()` `result` с объектом в качестве параметра. Если обратный `submitHandler` вызов был указан в `tasks.startTask()`Teams вызывает его в `result` качестве параметра. Если при вызове произошла `tasks.startTask()`ошибка, `submitHandler` функция вызывается со строкой `err` . <br/><br/> 3. Можно также указать значение при `completionBotId` вызове `teams.startTask()`. Затем он `result` отправляется боту. | 1. Вызовите функцию Teams клиентского пакета SDK `tasks.startTask()` с объектом [TaskInfo](#the-taskinfo-object) `TaskInfo.card` и содержащим JSON для адаптивной карточки, отображаемой во всплывающем окне модуля задач. <br/><br/> 2. `submitHandler` `tasks.startTask()``err` Если обратный вызов был указан в Teams вызывает его строкой, `tasks.startTask()` если при вызове произошла ошибка или пользователь закрывает всплывающее окно модуля задач с помощью X в правом верхнем углу. <br/><br/> 3. Если пользователь нажимает кнопку `Action.Submit` , `data` его объект возвращается в качестве значения `result`. |
| Кнопка карточки бота | 1. Кнопки карточки бота в зависимости от типа кнопки могут вызывать модули задач двумя способами: URL-адресом `task/fetch` глубокой ссылки или отправкой сообщения. <br/><br/> 2. Если `type` `task/fetch` `Action.Submit` действие кнопки является типом кнопки для адаптивных карточек, `task/fetch invoke` то боту отправляется событие HTTP POST. Бот отвечает на запрос POST с http 200 и текстом ответа, содержащим оболочку вокруг объекта [TaskInfo](#the-taskinfo-object). Дополнительные сведения см. [в статье о вызове модуля задач с помощью `task/fetch`](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch). Teams отображает модуль задачи. <br/><br/> 3. После выполнения пользователем действий вызовите функцию Teams SDK `tasks.submitTask()` с объектом `result` в качестве параметра. Бот получает сообщение, `task/submit invoke` содержащее `result` объект. <br/><br/> 4. `task/submit` У вас есть три разных способа реагирования на сообщение, не выполнив никаких действий, которые были успешно завершены задачей, отображая сообщение пользователю во всплывающем окне или вызывая другое окно модуля задач. Дополнительные сведения см [. в подробном обсуждении `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | <ul><li> Как и кнопки на карточках Bot Framework, кнопки на адаптивных карточках поддерживают два способа вызова модулей задач: `Action.openUrl` `task/fetch` `Action.Submit` URL-адреса глубоких ссылок с кнопками и использование кнопок. </li></ul> <br/><br/> <ul><li> Модули задач с адаптивными карточками работают так же, как htmL или JavaScript. Основное различие заключается в том, что, так как при использовании адаптивных карточек javaScript отсутствует, вызов невозможно `tasks.submitTask()`. Вместо этого Teams получает объект `data` `Action.Submit` и возвращает его в качестве полезных данных `task/submit` события. Дополнительные сведения см. [в статье о гибкости `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). </li></ul> |
| URL-адрес глубокой ссылки <br/>[синтаксис URL-адреса](#task-module-deep-link-syntax) | 1. Teams вызывает модуль задачи, который является URL-адресом `<iframe>` `url`, который отображается внутри указанного параметра глубокой ссылки. Обратный вызов `submitHandler` отсутствует. <br/><br/> 2. В JavaScript `tasks.submitTask()` `result` страницы в модуле задачи вызовите его, чтобы закрыть его с помощью объекта в качестве параметра, как при вызове с вкладки или кнопки карточки бота. Однако логика завершения немного отличается. Если логика завершения находится на клиенте, если бот отсутствует, `submitHandler` обратный вызов отсутствует, поэтому любая логика завершения должна находиться в коде, предшествующего вызову `tasks.submitTask()`. Сообщения об ошибках вызова отображаются только через консоль. Если у вас есть бот, можно указать параметр `completionBotId` в глубокой ссылке для отправки `result` объекта через `task/submit` событие. | 1. Teams вызывает модуль задачи, который является текстом карточки JSON адаптивной карточки, указанной в качестве значения параметра глубокой ссылки в кодировке URL`card`. <br/><br/> 2. Пользователь закрывает модуль задачи, щелкнув значок X `Action.Submit` в правом верхнем углу модуля задач или нажав кнопку на карточке. Так как нет `submitHandler` вызова, у пользователя должен быть бот для отправки значения полей адаптивной карточки. Пользователь должен использовать параметр в `completionBotId` глубокой ссылке, чтобы указать бота для отправки данных с помощью `task/submit invoke` события. |

В следующем разделе указывается объект `TaskInfo` , определяющий определенные атрибуты для модуля задачи.

## <a name="the-taskinfo-object"></a>Объект TaskInfo

Объект `TaskInfo` содержит метаданные для модуля задачи. Определите `url` внедренный iFrame или `card` адаптивную карточку. В следующей таблице приведено определение объекта:

| Атрибут | Тип | Описание |
| --- | --- | --- |
| `title` | string | Этот атрибут отображается под именем приложения и справа от значка приложения. |
| `height` | number или string | Этот атрибут может быть числом, представляющим высоту модуля задачи в пикселях, `small`или , `medium`или `large`. Дополнительные сведения см. в [описании размера модуля задач](#task-module-sizing). |
| `width` | number или string | Этот атрибут может быть числом, представляющим ширину модуля задачи в пикселях, `small`или , `medium`или `large`. Дополнительные сведения см. в [описании размера модуля задач](#task-module-sizing). |
| `url` | string | Этот атрибут является URL-адресом страницы, загруженной как внутри `<iframe>` модуля задачи. Домен URL-адреса должен находиться в массиве [validDomains](~/resources/schema/manifest-schema.md#validdomains) приложения в манифесте приложения. |
| `card` | Адаптивная карточка или вложение карточки бота адаптивной карточки | Этот атрибут является JSON для адаптивной карточки, отображаемой в модуле задачи. Если пользователь вызывает бота, используйте JSON адаптивной карточки в объекте Bot Framework `attachment` . На вкладке пользователь должен использовать адаптивную карточку. Дополнительные сведения см. в разделе ["Адаптивная карточка" или "Вложение карточки бота адаптивной карточки"](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | Строка | Этот атрибут открывает URL-адрес на вкладке браузера, если клиент не поддерживает функцию модуля задач. |
| `completionBotId` | Строка | Этот атрибут указывает идентификатор приложения бота для отправки результата взаимодействия пользователя с модулем задачи. Если этот параметр указан, бот получает `task/submit invoke` событие с объектом JSON в полезных данных события. |

> [!NOTE]
> Функция модуля задач требует, чтобы домены всех URL-адресов `validDomains` , которые вы хотите загрузить, были включены в массив в манифесте приложения.

В следующем разделе указывается размер модуля задач, позволяющий пользователю задать высоту и ширину модуля задачи.

## <a name="task-module-sizing"></a>Изменение размера модуля задач

С помощью целых чисел для `TaskInfo.width` и `TaskInfo.height`, задает высоту и ширину модуля задачи в пикселях. Однако в зависимости от размера окна команды и разрешения экрана они уменьшаются пропорционально, сохраняя пропорции ширины или высоты.

Если `TaskInfo.width` и `TaskInfo.height` `"small"`являются , `"medium"`или `"large"`, размер красного прямоугольника на следующем изображении является частью доступного пространства, 20 %, 50 % и 60 % для `width` и 20 %, 50 % и 66 % для `height`:

:::image type="content" source="../../assets/images/task-module/task-module-example.png" alt-text="Пример модуля задач":::

Модули задач, вызываемые с вкладки, можно динамически изменить размер. После вызова `tasks.startTask()` можно вызвать, `tasks.updateTask(newSize)` где свойства высоты и ширины объекта newSize соответствуют спецификации TaskInfo, например `{ height: 'medium', width: 'medium' }`.

В следующем разделе приведены примеры внедрения модулей задач в видео с YouTube и PowerApp.

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>CSS модуля задач для модулей задач HTML или JavaScript

Модули задач на основе HTML или JavaScript имеют доступ ко всей области модуля задач под заголовком. Хотя это обеспечивает большую гибкость, если вы хотите, чтобы заполнение по краям согласовывались с элементами заголовка и избегали ненужных полос прокрутки, пользователь должен предоставить правильный CSS. В следующих разделах приведены некоторые примеры для нескольких вариантов использования.

### <a name="example-1-youtube-video"></a>Пример 1. Видео с YouTube

YouTube предлагает возможность внедрять видео на веб-страницы. Вы можете легко внедрять видео на веб-страницы в модуль задач с помощью простой веб-страницы заглушки.

:::image type="content" source="../../assets/images/task-module/youtube-example.png" alt-text="Пример с Youtube":::

В следующем коде приведен пример HTML-кода для веб-страницы без CSS:

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

В следующем коде приведен пример CSS:

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

Пользователь также может использовать тот же подход для внедрения PowerApp. Так как высота или ширина любого отдельного приложения PowerApp настраиваются, пользователь может настроить высоту и ширину для достижения нужной презентации.

:::image type="content" source="../../assets/images/task-module/powerapp-example.png" alt-text="PowerApp":::

В следующем коде приведен пример HTML-кода для PowerApp:

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

В следующем коде приведен пример CSS:

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

В следующем разделе приводятся сведения о вызове карточки с помощью адаптивной карточки или вложения карточки бота адаптивной карточки.

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Адаптивная карточка или вложение карточки бота адаптивной карточки

В зависимости от `card`способа вызова необходимо использовать адаптивную карточку или вложение карточки бота адаптивной карточки, которая представляет собой адаптивную карточку, упакованную в объект вложения.

При вызове с вкладки пользователь должен использовать адаптивную карточку.

В следующем коде приведен пример адаптивной карточки:

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

В следующем коде приведен пример вложения карточки бота адаптивной карточки при вызове бота:

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

В следующем разделе приводятся сведения о синтаксисе глубокой `TaskInfo` связи модуля задач, включая объект и `APP_ID` `BOT_APP_ID`.

## <a name="task-module-deep-link-syntax"></a>Синтаксис глубокой связи модуля задач

Глубокая ссылка модуля задач — это сериализация объекта TaskInfo со следующими двумя другими сведениями и при `APP_ID` `BOT_APP_ID`необходимости :

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Типы данных и допустимые значения для `<TaskInfo.url>`объектов [TaskInfo](#the-taskinfo-object)`<TaskInfo.card>`, , `<TaskInfo.height>`, и`<TaskInfo.width>``<TaskInfo.title>`, см.

> [!TIP]
> URL-адрес кодирует прямую ссылку при использовании параметра`card`, например функцию [`encodeURI()` JavaScript.](https://www.w3schools.com/jsref/jsref_encodeURI.asp)

В следующей таблице приведены сведения о следующих параметрах `APP_ID` `BOT_APP_ID`:

| Значение | Тип | Обязательный | Описание |
| --- | --- | --- | --- |
| `APP_ID` | string | Да | Идентификатор [приложения](~/resources/schema/manifest-schema.md#id) , которое вызывает модуль задачи. Массив [validDomains в](~/resources/schema/manifest-schema.md#validdomains) манифесте должен `APP_ID` содержать `url` `url` домен, если он находится в URL-адресе. Идентификатор приложения уже известен при вызове модуля задачи с вкладки или бота, поэтому он не включен в .`TaskInfo` |
| `BOT_APP_ID` | string | Нет | Если задано значение `completionBotId` , `result` объект отправляется с помощью сообщения `task/submit invoke` указанному боту. `BOT_APP_ID` должен быть указан как бот в манифесте приложения, то есть его нельзя отправить ни в один бот. |

> [!NOTE]
> `APP_ID` и `BOT_APP_ID` может быть одинаковым во многих случаях, если приложение имеет рекомендуемый бот для использования в качестве идентификатора приложения, если он есть.

В следующем разделе приводятся сведения об использовании клавиатуры с модулем задач приложения.

## <a name="keyboard-and-accessibility-guidelines"></a>Рекомендации по использованию клавиатуры и специальных возможностей

С помощью модулей задач на основе HTML или JavaScript необходимо убедиться, что модуль задач приложения можно использовать с клавиатурой. Программы чтения с экрана также зависят от возможности навигации с помощью клавиатуры. Это включает в себя следующие два элемента:

* Использование [атрибута tabindex в](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/tabindex) тегах HTML для управления элементами, которые могут быть отсортированные. Кроме того, используйте атрибут табиндекса, чтобы определить, где он участвует в последовательной навигации с помощью клавиатуры, обычно с помощью клавиш <kbd>TAB</kbd> <kbd>и SHIFT-TAB</kbd> .
* Обработка <kbd>клавиши ESC</kbd> в JavaScript для модуля задачи. В следующем коде приведен пример обработки клавиши <kbd>ESC</kbd> :

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
|Пример bots-V4 для модуля задач | Примеры для создания модулей задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|Примеры вкладок модуля задач и bots-V3 | Примеры для создания модулей задач. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Использование модулей задач во вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

## <a name="see-also"></a>См. также

* [Запрос разрешений устройства](~/concepts/device-capabilities/native-device-permissions.md)
* [Интеграция возможностей мультимедиа](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Интеграция функции QR или сканера штрихкодов в Teams](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Интеграция функций местонахождения](~/concepts/device-capabilities/location-capability.md)
