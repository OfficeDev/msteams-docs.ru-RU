---
title: Вызов и закрытие модулей задач
description: Вызов и увольнение модулей задач.
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 88544199007b92b2f29d99153cde7bca760a44f3c92c7ce710cdd8db4ebff986
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2021
ms.locfileid: "57706647"
---
# <a name="invoke-and-dismiss-task-modules"></a>Вызов и закрытие модулей задач

Модули задач можно вызывать из вкладок, ботов или глубоких ссылок. Ответ может быть как в HTML, JavaScript, так и в качестве адаптивной карты. Существует большая гибкость с точки зрения вызова модулей задач и реагирования на взаимодействие пользователя. В следующей таблице кратко излагается, как это работает:

| Вызывается с помощью | Модуль задач с HTML или JavaScript | Модуль задач с адаптивной картой |
| --- | --- | --- |
| JavaScript на вкладке | 1. Используйте функцию Teams SDK с необязательной функцией `tasks.startTask()` `submitHandler(err, result)` вызова. <br/><br/> 2. В коде модуля задач, когда пользователь выполнил действия, вызываем функцию Teams SDK с объектом `tasks.submitTask()` `result` в качестве параметра. Если был указан вызов, Teams вызывает его `submitHandler` в качестве `tasks.startTask()` `result` параметра. Если при призыве произошла ошибка, функция `tasks.startTask()` `submitHandler` называется `err` строкой. <br/><br/> 3. Вы также можете указать при `completionBotId` вызове `teams.startTask()` . Затем вместо `result` этого отправляется бот. | 1. Вызов Teams клиентской SDK-функции с объектом TaskInfo и содержащим JSON для адаптивной карты, чтобы показать в всплывающее всплывающее представление модуля `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` задач. <br/><br/> 2. Если вызов был указан в , Teams вызывает его строкой, если произошла ошибка при вызове или если пользователь закрывает всплывающее всплывающее сообщение модуля задач с помощью X в правом верхнем `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` ряду. <br/><br/> 3. Если пользователь нажимает кнопку, его объект возвращается `Action.Submit` `data` в качестве значения `result` . |
| Кнопка карточки бота | 1. Кнопки бот-карты в зависимости от типа кнопки могут вызывать модули задач двумя способами: URL-адресом глубокой ссылки или отправкой `task/fetch` сообщения. <br/><br/> 2. Если действие кнопки является типом кнопки для адаптивных карт, событие HTTP POST отправляется `type` `task/fetch` `Action.Submit` `task/fetch invoke` боту. Бот отвечает на СООБЩЕНИЕ с помощью HTTP 200 и тело отклика, содержащее оболочку вокруг объекта [TaskInfo.](#the-taskinfo-object) Дополнительные сведения см. [в ссылке `task/fetch` на ссылку на модуль задач с помощью ](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch). Teams отображает модуль задач. <br/><br/> 3. После выполнения действий пользователем вызываем Teams SDK с объектом `tasks.submitTask()` `result` в качестве параметра. Бот получает `task/submit invoke` сообщение, содержаное `result` объект. <br/><br/> 4. У вас есть три различных способа ответа на сообщение, не делая ничего, что является успешно выполненной задачей, отобразив сообщение пользователю в всплывающее окно или путем запроса другого окна модуля `task/submit` задач. Дополнительные сведения см. в [подробном обсуждении. `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit) | <ul><li> Как и кнопки на картах Bot Framework, кнопки адаптивных карт поддерживают два способа вызова модулей задач, глубокие ссылки URL-адресов с кнопками и использование `Action.openUrl` `task/fetch` `Action.Submit` кнопок. </li></ul> <br/><br/> <ul><li> Модули задач с адаптивными картами работают очень похоже на HTML или JavaScript. Главное отличие состоит в том, что, поскольку при использовании адаптивных карт javaScript нет javaScript, звонить `tasks.submitTask()` нельзя. Вместо этого Teams принимает объект и возвращает его в качестве `data` `Action.Submit` полезной нагрузки `task/submit` события. Дополнительные сведения см. [в дополнительных `task/submit` сведениях. ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit) </li></ul> |
| URL-адрес глубокой ссылки <br/>[синтаксис URL-адреса](#task-module-deep-link-syntax) | 1. Teams вызывает модуль задач, который является URL-адресом, который отображается внутри указанного в параметре `<iframe>` `url` глубокой ссылки. Нет `submitHandler` вызова. <br/><br/> 2. В JavaScript страницы в модуле задач позвоните, чтобы закрыть его с объектом в качестве параметра, так же, как при вызове его с вкладки или кнопки карты `tasks.submitTask()` `result` бота. Однако логика завершения несколько отличается. Если логика завершения находится на клиенте, если бота нет, нет вызова, поэтому любая логика завершения должна быть в коде, предшествующего `submitHandler` `tasks.submitTask()` вызову. Ошибки вызовов сообщаются только через консоль. Если у вас есть бот, можно указать параметр в глубокой ссылке, чтобы `completionBotId` отправить `result` объект через `task/submit` событие. | 1. Teams вызывает модуль задач, который является телом карточки JSON адаптивной карты, заданным как url-кодированное значение параметра `card` глубокой ссылки. <br/><br/> 2. Пользователь закрывает модуль задач, выбрав X в правом верхнем справа от модуля задачи или нажав кнопку `Action.Submit` на карточке. Так как нет вызова, у пользователя должен быть бот для отправки значения `submitHandler` полей адаптивной карты. Пользователь должен использовать параметр в глубокой ссылке, чтобы указать бота, чтобы отправить данные `completionBotId` с помощью `task/submit invoke` события. |

> [!NOTE]
> Призыв к модульу задач из JavaScript не поддерживается на мобильных устройствах.

В следующем разделе указывается объект, который определяет `TaskInfo` определенные атрибуты для модуля задач.

## <a name="the-taskinfo-object"></a>Объект TaskInfo

Объект `TaskInfo` содержит метаданные для модуля задач. Определите `url` для встроенного iFrame или `card` адаптивной карты. В следующей таблице содержится определение объекта:

| Атрибут | Тип | Описание |
| --- | --- | --- |
| `title` | string | Этот атрибут отображается ниже имени приложения и справа от значка приложения. |
| `height` | number или string | Этот атрибут может быть числом, представляющим высоту модуля задач в пикселях, или `small` , `medium` или `large` . Дополнительные сведения см. [в деле размеров модуля задач.](#task-module-sizing) |
| `width` | number или string | Этот атрибут может быть числом, представляющим ширину модуля задач в пикселях, или `small` `medium` , или `large` . Дополнительные сведения см. [в деле размеров модуля задач.](#task-module-sizing) |
| `url` | string | Этот атрибут — URL-адрес страницы, загружаемой в `<iframe>` модуль задач. Домен URL-адреса должен быть в массиве [validDomains](~/resources/schema/manifest-schema.md#validdomains) приложения в манифесте приложения. |
| `card` | Адаптивная карта или вложение бота адаптивной карты | Этот атрибут — JSON для адаптивной карты, которая появится в модуле задач. Если пользователь отзовется от бота, используйте адаптивную карту JSON в объекте Bot `attachment` Framework. На вкладке пользователь должен использовать адаптивную карту. Дополнительные сведения см. в [вложении в бот-карту Adaptive Card или Adaptive Card.](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | Этот атрибут открывает URL-адрес на вкладке браузера, если клиент не поддерживает функцию модуля задач. |
| `completionBotId` | string | Этот атрибут указывает бот-ID приложения для отправки результатов взаимодействия пользователя с модулем задач. Если указано, бот получает событие с объектом `task/submit invoke` JSON в полезной нагрузке события. |

> [!NOTE]
> Функция модуля задач требует, чтобы домены всех URL-адресов, которые необходимо загрузить, были включены в массив `validDomains` манифеста приложения.

В следующем разделе указывается размер модуля задач, который позволяет пользователю устанавливать высоту и ширину модуля задач.

## <a name="task-module-sizing"></a>Размер модуля задач

Использование целого набора для и , задает высоту и ширину модуля `TaskInfo.width` `TaskInfo.height` задач в пикселях. Однако в зависимости от размера окна и разрешения экрана команды они уменьшаются пропорционально при сохранении соотношения аспектов шириной или высотой.

Если и являются , или , размер красного прямоугольника в следующем изображении является частью доступного `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` пространства, 20%, 50%, и 60% для `width` и 20%, 50%, и 66% для `height` :

![Пример модуля задач](~/assets/images/task-module/task-module-example.png)

Модули задач, вызываемые со вкладки, можно динамически реамизировать. После вызова можно вызвать, где свойства высоты и ширины объекта `tasks.startTask()` `tasks.updateTask(newSize)` newSize соответствуют спецификации TaskInfo, например `{ height: 'medium', width: 'medium' }` .

В следующем разделе приводится пример встраив модулей задач в видео YouTube и PowerApp.

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>Модуль задач CSS для модулей задач HTML или JavaScript

Модули задач на основе HTML или JavaScript имеют доступ ко всей области модуля задач ниже заголовка. Хотя это обеспечивает большую гибкость, если вы хотите, чтобы обивка по краям совпадала с элементами заголовки и избегала ненужных свитков, пользователь должен предоставить правильный CSS. В следующих разделах вы можете привести несколько примеров для нескольких примеров использования.

**Пример 1. Видео На YouTube**

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

**Пример 2. PowerApp**

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

В зависимости от того, как вы назовете, необходимо использовать адаптивную карту или вложение бота адаптивной карты, которая является адаптивной картой, завернутой в объект `card` вложения.

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

В следующем разделе приводится подробная информация о синтаксисе глубокой ссылки модуля задач, включая `TaskInfo` объект и `APP_ID` `BOT_APP_ID` .

## <a name="task-module-deep-link-syntax"></a>Синтаксис глубокой ссылки модуля задач

Глубокая ссылка модуля задач — это сериализация объекта TaskInfo со следующими двумя другими деталями и необязательно `APP_ID` `BOT_APP_ID` :

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Для типов данных и допустимых значений `<TaskInfo.url>` для , , , и , `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` [см. объект TaskInfo](#the-taskinfo-object).

> [!TIP]
> URL-адрес кодирует глубокую ссылку при использовании `card` параметра, например [ `encodeURI()` ](https://www.w3schools.com/jsref/jsref_encodeURI.asp)функции JavaScript.

В следующей таблице приводится информация о `APP_ID` `BOT_APP_ID` и:

| Значение | Тип | Обязательный | Описание |
| --- | --- | --- | --- |
| `APP_ID` | string | Да | ID [приложения,](~/resources/schema/manifest-schema.md#id) выдавлив модуль задач. Массив [validDomains в](~/resources/schema/manifest-schema.md#validdomains) манифесте для должен содержать домен, если `APP_ID` находится в `url` `url` URL-адресе. ID приложения уже известен, когда модуль задач вызывается со вкладки или бота, поэтому он не включен `TaskInfo` в . |
| `BOT_APP_ID` | string | Нет | Если задано значение, объект отправляется с `completionBotId` `result` помощью сообщения `task/submit invoke` указанному боту. `BOT_APP_ID` должно быть указано как бот в манифесте приложения, то есть вы не можете отправить его любому боту. |

> [!NOTE]
> `APP_ID` и может быть одинаковым во многих случаях, если у приложения есть рекомендуемый бот для использования в качестве `BOT_APP_ID` ID приложения, если он есть.

В следующем разделе приводится подробная информация об использовании клавиатуры с модулем задач вашего приложения.

## <a name="keyboard-and-accessibility-guidelines"></a>Рекомендации по клавиатуре и доступности

С помощью модулей задач на основе HTML или JavaScript необходимо убедиться, что модуль задач вашего приложения можно использовать с помощью клавиатуры. Программы чтения с экрана также зависят от возможности навигации с помощью клавиатуры. Это включает в себя следующие две вещи:

* Использование [атрибута tabindex в](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) тегах HTML для управления элементами, которые могут быть сфокусированы. Кроме того, используйте атрибут tabindex, чтобы определить, где он участвует в последовательной навигации клавиатуры обычно с <kbd>клавишами Tab</kbd> и <kbd>Shift-Tab.</kbd>
* Обработка <kbd>ключа Esc</kbd> в JavaScript для модуля задач. В следующем коде приводится пример обработки ключа <kbd>Esc:</kbd>

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
|Пример модуля задач bots-V4 | Примеры для создания модулей задач. |[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|Пример вкладок модуля задач и ботов-V3 | Примеры для создания модулей задач. |[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a>Дополнительные ресурсы

* [Запрос разрешений устройства](~/concepts/device-capabilities/native-device-permissions.md)
* [Интеграция возможностей мультимедиа](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Интеграция возможностей сканера QR или штрихкодов в Teams](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Интеграция возможностей расположения в Teams](~/concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Использование модулей задач во вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md)