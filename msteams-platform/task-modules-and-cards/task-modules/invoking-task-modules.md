---
title: Вызов и закрытие модулей задач
description: Сведения о ссылке и отклонении модулей задач, объекта информации о задачах, размере модуля задач, синтаксис глубокой ссылки модуля задач с помощью образцов кода
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 84cca74d6e81dce9bbcd7637b5d0b6537524d831
ms.sourcegitcommit: a36760750ff4f510c374a4c956be57f7c1b4a0db
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/20/2022
ms.locfileid: "63674728"
---
# <a name="invoke-and-dismiss-task-modules"></a>Вызов и закрытие модулей задач

Модули задач можно вызывать из вкладок, ботов или глубоких ссылок. Ответ может быть как в HTML, JavaScript, так и в качестве адаптивной карты. Существует большая гибкость с точки зрения вызова модулей задач и реагирования на взаимодействие пользователя. В следующей таблице кратко излагается, как это работает:

| Вызывается с помощью | Модуль задач с HTML или JavaScript | Модуль задач с адаптивной картой |
| --- | --- | --- |
| JavaScript на вкладке | 1. Используйте функцию Teams SDK с `tasks.startTask()` необязательной `submitHandler(err, result)` функцией вызова. <br/><br/> 2. В коде модуля задач, когда пользователь выполнил действия, вызываем функцию Teams SDK `tasks.submitTask()` `result` с объектом в качестве параметра. Если был `submitHandler` указан вызов`tasks.startTask()`, Teams вызывает его в `result` качестве параметра. Если при призыве произошла `tasks.startTask()`ошибка, `submitHandler` функция называется `err` строкой. <br/><br/> 3. Вы также можете указать при вызове `completionBotId` `teams.startTask()`. Затем вместо `result` этого отправляется бот. | 1. Вызов Teams клиентской функции SDK `tasks.startTask()` с объектом [TaskInfo](#the-taskinfo-object) `TaskInfo.card` и содержащей JSON для адаптивной карты, чтобы показать в всплывающее всплывающее представление модуля задач. <br/><br/> 2. `submitHandler` `tasks.startTask()`Если вызов был указан в , Teams `err` вызывает его строкой, `tasks.startTask()` если произошла ошибка при вызове или если пользователь закрывает всплывающее всплывающее сообщение модуля задач с помощью X в правом верхнем ряду. <br/><br/> 3. Если пользователь нажимает кнопку `Action.Submit` , `data` его объект возвращается в качестве значения `result`. |
| Кнопка карточки бота | 1. Кнопки бот-карты в зависимости от типа кнопки могут вызывать модули задач двумя способами: `task/fetch` URL-адресом глубокой ссылки или отправкой сообщения. <br/><br/> 2. Если `type` `task/fetch` `Action.Submit` действие кнопки является типом кнопки для адаптивных карт, `task/fetch invoke` событие HTTP POST отправляется боту. Бот отвечает на СООБЩЕНИЕ с помощью HTTP 200 и тело отклика, содержащее оболочку вокруг объекта [TaskInfo](#the-taskinfo-object). Дополнительные сведения см. [в ссылке на ссылку на модуль задач с помощью `task/fetch`](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch). Teams отображает модуль задач. <br/><br/> 3. После выполнения действий пользователем вызываем Teams SDK `tasks.submitTask()` `result` с объектом в качестве параметра. Бот получает сообщение, `task/submit invoke` содержаное объект `result` . <br/><br/> 4. `task/submit` У вас есть три различных способа ответа на сообщение, не делая ничего, что является успешно выполненной задачей, отобразив сообщение пользователю в всплывающее окно или путем запроса другого окна модуля задач. Дополнительные сведения см. в [подробном обсуждении `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | <ul><li> Как и кнопки на картах Bot Framework, кнопки адаптивных карт поддерживают два способа вызова модулей задач, глубокие ссылки URL-адресов `Action.openUrl` `task/fetch` `Action.Submit` с кнопками и использование кнопок. </li></ul> <br/><br/> <ul><li> Модули задач с адаптивными картами работают очень похоже на HTML или JavaScript. Главное отличие состоит в том, что, поскольку при использовании адаптивных карт javaScript нет javaScript, `tasks.submitTask()`звонить нельзя. Вместо этого Teams принимает `data` `Action.Submit` объект и возвращает его в качестве полезной нагрузки `task/submit` события. Дополнительные сведения см. [в дополнительных сведениях.`task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit) </li></ul> |
| URL-адрес глубокой ссылки <br/>[синтаксис URL-адреса](#task-module-deep-link-syntax) | 1. Teams вызывает модуль задач, который является URL-адресом `<iframe>` `url`, который отображается внутри указанного в параметре глубокой ссылки. Нет вызова `submitHandler` . <br/><br/> 2. В JavaScript `tasks.submitTask()` `result` страницы в модуле задач позвоните, чтобы закрыть его с объектом в качестве параметра, так же, как при вызове его с вкладки или кнопки карты бота. Однако логика завершения несколько отличается. Если логика завершения находится на клиенте, если бота нет, `submitHandler` нет вызова, поэтому любая логика завершения должна быть в коде, предшествующего вызову `tasks.submitTask()`. Ошибки вызовов сообщаются только через консоль. Если у вас есть бот, можно `completionBotId` указать параметр в глубокой ссылке, чтобы отправить `result` объект через `task/submit` событие. | 1. Teams вызывает модуль задач, который является телом карточки JSON адаптивной карты, заданным как кодированное URL-адресом `card` значение параметра глубокой ссылки. <br/><br/> 2. Пользователь закрывает модуль задач, выбрав X `Action.Submit` в правом верхнем справа от модуля задачи или нажав кнопку на карточке. Так как нет `submitHandler` вызова, у пользователя должен быть бот для отправки значения полей адаптивной карты. Пользователь должен использовать параметр в `completionBotId` глубокой ссылке, чтобы указать бота, чтобы отправить данные с помощью `task/submit invoke` события. |

В следующем разделе указывается `TaskInfo` объект, который определяет определенные атрибуты для модуля задач.

## <a name="the-taskinfo-object"></a>Объект TaskInfo

Объект `TaskInfo` содержит метаданные для модуля задач. Определите `url` для встроенного iFrame или `card` адаптивной карты. В следующей таблице содержится определение объекта:

| Атрибут | Тип | Описание |
| --- | --- | --- |
| `title` | string | Этот атрибут отображается ниже имени приложения и справа от значка приложения. |
| `height` | number или string | Этот атрибут может быть числом, представляющим высоту модуля задач в пикселях, `small`или , или `large``medium`. Дополнительные сведения см. в [области размеров модуля задач](#task-module-sizing). |
| `width` | number или string | Этот атрибут может быть числом, представляющим ширину модуля задач в пикселях, `small`или , или `large``medium`. Дополнительные сведения см. в [области размеров модуля задач](#task-module-sizing). |
| `url` | string | Этот атрибут — URL-адрес страницы, загружаемой в модуль `<iframe>` задач. Домен URL-адреса должен быть в массиве [validDomains](~/resources/schema/manifest-schema.md#validdomains) приложения в манифесте приложения. |
| `card` | Адаптивная карта или вложение бота адаптивной карты | Этот атрибут — JSON для адаптивной карты, которая появится в модуле задач. Если пользователь отзовется от бота, используйте адаптивную карту JSON в объекте Bot Framework `attachment` . На вкладке пользователь должен использовать адаптивную карту. Дополнительные сведения см. в [вложении в бот-карту Adaptive Card или Adaptive Card](#adaptive-card-or-adaptive-card-bot-card-attachment). |
| `fallbackUrl` | string | Этот атрибут открывает URL-адрес на вкладке браузера, если клиент не поддерживает функцию модуля задач. |
| `completionBotId` | string | Этот атрибут указывает бот-ID приложения для отправки результатов взаимодействия пользователя с модулем задач. Если указано, бот получает `task/submit invoke` событие с объектом JSON в полезной нагрузке события. |

> [!NOTE]
> Функция модуля задач требует, чтобы домены всех URL-адресов `validDomains` , которые необходимо загрузить, были включены в массив манифеста приложения.

В следующем разделе указывается размер модуля задач, который позволяет пользователю устанавливать высоту и ширину модуля задач.

## <a name="task-module-sizing"></a>Размер модуля задач

Использование целого набора для и `TaskInfo.width` `TaskInfo.height`, задает высоту и ширину модуля задач в пикселях. Однако в зависимости от размера окна и разрешения экрана команды они уменьшаются пропорционально при сохранении соотношения аспектов шириной или высотой.

Если и являются , `"medium"``"large"`или , размер красного прямоугольника в следующем изображении является частью доступного пространства, 20%, 50%, и 60% для `width` и 20%, 50%, и 66% для `height`:`TaskInfo.width` `TaskInfo.height` `"small"`

![Пример модуля задач](~/assets/images/task-module/task-module-example.png)

Модули задач, вызываемые со вкладки, можно динамически реамизировать. После вызова `tasks.startTask()` можно вызвать, `tasks.updateTask(newSize)` где свойства высоты и ширины объекта newSize соответствуют спецификации TaskInfo, например `{ height: 'medium', width: 'medium' }`.

В следующем разделе приводится пример встраив модулей задач в видео YouTube и PowerApp.

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>Модуль задач CSS для модулей задач HTML или JavaScript

Модули задач на основе HTML или JavaScript имеют доступ ко всей области модуля задач ниже заголовка. Хотя это обеспечивает большую гибкость, если вы хотите, чтобы обивка по краям совпадала с элементами заголовки и избегала ненужных свитков, пользователь должен предоставить правильный CSS. В следующих разделах вы можете привести несколько примеров для нескольких примеров использования.

### <a name="example-1-youtube-video"></a>Пример 1. Видео На YouTube

YouTube предлагает возможность встраить видео на веб-страницах. Легко встраить видео на веб-страницах в модуль задач с помощью простой веб-страницы забоя.

![Видео YouTube](~/assets/images/task-module/youtube-example.png)

В следующем коде приводится пример HTML для веб-страницы без CSS:

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

В следующем коде приводится пример CSS:

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

Для встраить PowerApp пользователь может использовать тот же подход. Поскольку высота или ширина любого отдельного PowerApp настраиваются, пользователь может настроить высоту и ширину для достижения нужной презентации.

![PowerApp управления активами](~/assets/images/task-module/powerapp-example.png)

В следующем коде приводится пример HTML для PowerApp:

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

В следующем коде приводится пример CSS:

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

В следующем разделе приводится подробная информация об отзове вашей карты с помощью адаптивной карты или вложения бот-карты адаптивной карты.

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Адаптивная карта или вложение бота адаптивной карты

В зависимости от `card`того, как вы назовете, необходимо использовать адаптивную карту или вложение бота адаптивной карты, которая является адаптивной картой, завернутой в объект вложения.

При наводке со вкладки пользователю необходимо использовать адаптивную карту.

В следующем коде приводится пример адаптивной карты:

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

В следующем коде приводится пример вложения бот-карты адаптивной карты при наложении от бота:

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

В следующем разделе приводится подробная информация о синтаксисе `TaskInfo` глубокой ссылки модуля задач, включая объект и `APP_ID` `BOT_APP_ID`.

## <a name="task-module-deep-link-syntax"></a>Синтаксис глубокой ссылки модуля задач

Глубокая ссылка модуля задач — это сериализация объекта TaskInfo со следующими двумя другими деталями и `APP_ID` `BOT_APP_ID`необязательно :

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Для типов данных и допустимых значений `<TaskInfo.url>`для , `<TaskInfo.card>`, , `<TaskInfo.height>`и `<TaskInfo.width>`, см`<TaskInfo.title>`[. объект TaskInfo](#the-taskinfo-object).

> [!TIP]
> URL-адрес кодирует глубокую ссылку `card` при использовании параметра, например функции JavaScript[`encodeURI()`.](https://www.w3schools.com/jsref/jsref_encodeURI.asp)

В следующей таблице приводится информация о `APP_ID` и `BOT_APP_ID`:

| Значение | Тип | Обязательный | Описание |
| --- | --- | --- | --- |
| `APP_ID` | string | Да | [ID приложения](~/resources/schema/manifest-schema.md#id), выдавлив модуль задач. Массив [validDomains в](~/resources/schema/manifest-schema.md#validdomains) манифесте для `APP_ID` должен содержать домен `url` `url` , если находится в URL-адресе. ID приложения уже известен, когда модуль задач вызывается со вкладки или бота, поэтому он не включен `TaskInfo`в . |
| `BOT_APP_ID` | string | Нет | Если задано `completionBotId` значение, `result` объект отправляется с помощью сообщения `task/submit invoke` указанному боту. `BOT_APP_ID` должно быть указано как бот в манифесте приложения, то есть вы не можете отправить его любому боту. |

> [!NOTE]
> `APP_ID` и `BOT_APP_ID` может быть одинаковым во многих случаях, если у приложения есть рекомендуемый бот для использования в качестве ID приложения, если он есть.

В следующем разделе приводится подробная информация об использовании клавиатуры с модулем задач вашего приложения.

## <a name="keyboard-and-accessibility-guidelines"></a>Рекомендации по клавиатуре и доступности

С помощью модулей задач на основе HTML или JavaScript необходимо убедиться, что модуль задач вашего приложения можно использовать с помощью клавиатуры. Программы чтения с экрана также зависят от возможности навигации с помощью клавиатуры. Это включает в себя следующие две вещи:

* Использование [атрибута tabindex в](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/tabindex) тегах HTML для управления элементами, которые могут быть сфокусированы. Кроме того, используйте атрибут tabindex, чтобы определить, где он участвует в последовательной навигации клавиатуры обычно с <kbd>клавишами Tab</kbd> и <kbd>Shift-Tab</kbd> .
* Обработка <kbd>ключа Esc</kbd> в JavaScript для модуля задач. В следующем коде приводится пример обработки ключа <kbd>Esc</kbd> :

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teams обеспечивает правильную работу навигации по клавиатуре из заголовка модуля задач в HTML и наоборот.

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Пример модуля задач bots-V4 | Примеры для создания модулей задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|Пример вкладок модуля задач и ботов-V3 | Примеры для создания модулей задач. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Использование модулей задач во вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

## <a name="see-also"></a>См. также

* [Запрос разрешений устройства](~/concepts/device-capabilities/native-device-permissions.md)
* [Интеграция возможностей мультимедиа](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Интеграция возможностей сканера QR или штрихкодов в Teams](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Интеграция возможностей расположения в Teams](~/concepts/device-capabilities/location-capability.md)
