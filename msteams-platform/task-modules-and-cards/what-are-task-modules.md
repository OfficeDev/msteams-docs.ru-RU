---
title: Что такое модули задач?
author: clearab
description: Добавьте модули всплывающих приложений для сбора или отображения данных пользователям из Microsoft Teams приложений
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 23157e30ce25c2dfa1c21e7f5c4ddd4f735b660f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566845"
---
# <a name="task-modules"></a>Модули задач

Модули задач позволяют создавать модальные всплывающие окна в приложении Teams. В всплывающее всплывающее представление можно запустить собственный пользовательский код HTML/JavaScript, показать виджет на основе, например видео YouTube или Microsoft Stream, или отобразить `<iframe>` [адаптивную карту.](/adaptive-cards/) Они особенно полезны для инициа-ния и выполнения задач или отображения богатой информации, например видео или Power BI панелей мониторинга. Всплывающее впечатление часто более естественно для пользователей, которые инициировали и завершали задачи по сравнению с вкладками или ботами на основе беседы.

Модули задач строятся на основе вкладок Microsoft Teams; по сути это вкладка в окне всплывающее окно. Они используют один и тот же SDK, поэтому если вы создали вкладку, вы уже на 90% сможете создать модуль задач.

Модули задач можно вызывать тремя способами:

* **Вкладки** каналов или личных данных. С помощью Microsoft Teams tabs SDK можно вызвать модули задач из кнопок, ссылок или меню на вкладке. Это подробно [здесь.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **Bots:** Кнопки на [карточках,](~/task-modules-and-cards/cards/cards-reference.md) отправленных с вашего бота. Это особенно полезно, если вам не нужно, чтобы все в канале видели, что вы делаете с ботом. Например, когда вам нужно собрать ответы пользователей на опрос в канале, нет никакой необходимости отображать пошаговые действия по созданию этого опроса.  [Это подробно повеяно здесь.](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **За пределами Teams** из глубокой ссылки: можно также создавать URL-адреса для вызова модуля задач из любой точки. [Это подробно повеяно здесь.](#task-module-deep-link-syntax)

## <a name="task-module-looks-like"></a>Модуль задач выглядит так

Вот как выглядит модуль задач при вызове из бота (без цветных прямоугольников и нудных кругов, конечно):

![Пример модуля задач](~/assets/images/task-module/task-module-example.png)

Давайте пройдитесь по ней:

1. Значок [ `color` приложения](~/resources/schema/manifest-schema.md#icons).
1. Имя [ `short` приложения.](~/resources/schema/manifest-schema.md#name)
1. Название модуля задач, указанное в `title` свойстве объекта [TaskInfo.](#the-taskinfo-object)
1. Кнопка закрыть или отменить модуль задач. Если пользователь нажал это, ваше приложение получит `err` событие, как описано [здесь](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module).
    > [!Note]
    > В настоящее время невозможно обнаружить это событие при вызове модуля задач из бота.
1. Синий прямоугольник — это место, на котором отображается веб-страница при загрузке собственной веб-страницы с помощью свойства объекта `url` [TaskInfo.](#the-taskinfo-object) Дополнительные подробности приведены в [разделе размеров модуля задач](#task-module-sizing) ниже.
1. Если вы отображаете адаптивную карту с помощью свойства объекта `card` [TaskInfo,](#the-taskinfo-object) для вас добавляется обивка, в противном случае вам потребуется самостоятельно справиться [с этим.](#task-module-css-for-htmljavascript-task-modules)
1. Здесь будут отрисовываться кнопки адаптивной карты. Если вы используете собственную страницу, необходимо создать собственные кнопки.

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>Обзор наводки и увольнения модулей задач

Модули задач могут вызываться из вкладок, ботов или глубоких ссылок, а то, что появляется в одном, может быть HTML или адаптивной картой, поэтому существует большая гибкость с точки зрения того, как они вызываются и как справляться с результатом взаимодействия пользователя. В приведенной ниже таблице кратко излагается, как это работает:

| **Вызывается с помощью...** | **Модуль задач — HTML/JavaScript** | **Модуль задач — это адаптивная карта** |
| --- | --- | --- |
| **JavaScript на вкладке** | 1. Используйте функцию Teams SDK с необязательной функцией `tasks.startTask()` `submitHandler(err, result)` вызова. <br/><br/> 2. В коде модуля задач по завершению пользователя вызываем функцию Teams SDK с объектом `tasks.submitTask()` `result` в качестве параметра. Если был указан вызов, Teams вызывает его `submitHandler` в качестве `tasks.startTask()` `result` параметра.<br/><br/> 3. Если при призыве произошла ошибка, функция `tasks.startTask()` `submitHandler` называется `err` строкой. <br/><br/> 4. Вы также можете указать при вызове — в этом `completionBotId` `teams.startTask()` случае `result` отправляется боту. | 1. Вызов Teams клиентской функции SDK с объектом TaskInfo и содержащим JSON для адаптивной карты, чтобы показать в всплывающее всплывающее представление модуля `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` задач. <br/><br/> 2. Если вызов был указан в , Teams вызывает его строкой, если произошла ошибка при вызове или если пользователь закрывает всплывающее всплывающее сообщение модуля задач с помощью X в правом верхнем `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` ряду. <br/><br/> 3. Если пользователь нажал кнопку Action.Submit, его объект возвращается в качестве `data` значения `result` . |
| **Кнопка карточки бота** | 1. Кнопки бот-карты в зависимости от типа кнопки могут вызывать модули задач двумя способами: URL-адресом глубокой ссылки или отправкой `task/fetch` сообщения. См. ниже, как работают URL-адреса глубоких ссылок. <br/><br/> 2. Если действие кнопки (тип кнопки для адаптивных карт), событие (HTTP POST под крышками) отправляется боту, и бот отвечает на СООБЩЕНИЕ с `type` `task/fetch` HTTP `Action.Submit` `task/fetch invoke` 200 и телом ответа, содержащим оболочку вокруг объекта [TaskInfo](#the-taskinfo-object). Это подробно объясняется при взводе модуля задач [через задачу/извлечение](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-through-taskfetch).<br/><br/> 3. Teams отображает модуль задач; Когда пользователь закончит работу, позвоните Teams SDK с `tasks.submitTask()` `result` объектом в качестве параметра. <br/><br/> 4. Бот получает `task/submit invoke` сообщение, содержаное `result` объект. У вас есть три различных способа ответа на сообщение: ничего не делать (задача выполнена успешно), отобразив сообщение пользователю в всплывающее окно, или путем ссылки на другое окно модуля задач (например, создание мастера, как `task/submit` опыт). Эти три варианта более подробно обсуждаются [в подробном обсуждении задачи/отправки.](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit) | 1. Как и кнопки на картах Bot Framework, кнопки на адаптивных картах поддерживают два способа вызова модулей задач: глубокие ссылки URL-адресов с кнопками и с помощью `Action.openUrl` `task/fetch` `Action.Submit` кнопок. <br/><br/> 2. Модули задач с адаптивными картами работают очень аналогично делу HTML/JavaScript (см. слева). Главное отличие состоит в том, что, поскольку JavaScript не используется при использовании адаптивных карт, звонить `tasks.submitTask()` нельзя. Вместо этого Teams принимает объект и возвращает его в качестве полезной нагрузки в `data` `Action.Submit` событии, как `task/submit` описано [здесь](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). |
| **URL-адрес глубокой ссылки** <br/>[синтаксис URL-адреса](#task-module-deep-link-syntax) | 1. Teams вызывает модуль задач; URL-адрес, который отображается внутри `<iframe>` указанного в `url` параметре глубокой ссылки. Нет `submitHandler` вызова. <br/><br/> 2. В JavaScript страницы в модуле задач позвоните, чтобы закрыть его с объектом в качестве параметра, так же, как при вызове его с вкладки или кнопки карты `tasks.submitTask()` `result` бота. Однако логика завершения несколько отличается. Если логика завершения находится на клиенте (например, если бота нет) не будет вызова, поэтому любая логика завершения должна быть в коде, предшествующего `submitHandler` `tasks.submitTask()` вызову. О ошибках вызовов сообщается только через консоль. Если у вас есть бот, можно указать параметр в глубокой ссылке, чтобы `completionBotId` отправить объект с помощью `result` `task/submit` события. | 1. Teams вызывает модуль задач; Тело карточки JSON адаптивной карты указывается как url-кодированное значение параметра `card` глубокой ссылки. <br/><br/> 2. Пользователь закрывает модуль задач, щелкнув X в правом верхнем справа от модуля задачи или нажав кнопку `Action.Submit` на карточке. Так как нет вызова, необходимо иметь бота для отправки значения полей `submitHandler` адаптивной карты. Параметр в глубокой ссылке используется для указания бота для отправки данных `completionBotId` через `task/submit invoke` событие. |

## <a name="the-taskinfo-object"></a>Объект TaskInfo

Объект `TaskInfo` содержит метаданные для модуля задач. Определение объекта приведено ниже. Необходимо **определить** для `url` встроенного iFrame или `card` адаптивной карты.

| Атрибут | Тип | Описание |
| --- | --- | --- |
| `title` | string | Отображается ниже имени приложения и справа от значка приложения. |
| `height` | number или string | Это может быть число, представляющее высоту модуля задач в пикселях, или `small` `medium` , или `large` . [См. ниже, как обрабатываются высота и ширина.](#task-module-sizing) |
| `width` | number или string | Это может быть число, представляющее ширину модуля задач в пикселях, или `small` `medium` , или `large` . [См. ниже, как обрабатываются высота и ширина.](#task-module-sizing) |
| `url` | Строка | URL-адрес страницы, загруженной как `<iframe>` внутри модуля задач. Домен URL-адреса должен быть в массиве [validDomains](~/resources/schema/manifest-schema.md#validdomains) приложения в манифесте приложения. |
| `card` | Адаптивная карта или вложение бот-карты адаптивной карты | JSON для адаптивной карты, которая появится в модуле задач. Если вы назовете бота, вам потребуется использовать адаптивную карту JSON в объекте Bot `attachment` Framework. На вкладке вы будете использовать только адаптивную карту. [Вот пример.](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | Строка | Если клиент не поддерживает функцию модуля задач, этот URL-адрес открывается на вкладке браузера. |
| `completionBotId` | Строка | Указывает ID приложения-бота для отправки результатов взаимодействия пользователя с модулем задач. Если указано, бот получит событие с объектом `task/submit invoke` JSON в полезной нагрузке события. |

> [!NOTE]
> Функция модуля задач требует, чтобы домены всех URL-адресов, которые необходимо загрузить, были включены в массив `validDomains` манифеста приложения.

## <a name="task-module-sizing"></a>Размер модуля задач

Использование integers для `TaskInfo.width` и `TaskInfo.height` будет устанавливать высоту и ширину в пикселях. Однако в зависимости от размера окна и разрешения экрана группы они будут уменьшаться пропорционально при сохранении соотношения аспектов (ширина и высота).

Если и являются, или размер красного прямоугольника на рисунке выше, это доля доступного `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` пространства: 20%, 50%, 60% для и `width` 20%, 50%, 66% для `height` .

Модули задач, вызываемые со вкладки, можно динамически реамизировать. После вызова можно вызвать, где свойства высоты и ширины объекта newSize соответствуют спецификации `tasks.startTask()` `tasks.updateTask(newSize)` TaskInfo (например. `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>Модуль задач CSS для модулей задач HTML/JavaScript

Модули задач на основе HTML/JavaScript имеют доступ ко всей области модуля задач под заголовщиком. Хотя это обеспечивает большую гибкость, если вы хотите, чтобы обивка по краям совпадала с элементами загона и избегала ненужных прокруток, необходимо предоставить правильный CSS. Вот несколько примеров для нескольких случаев использования.

### <a name="example-1---youtube-video"></a>Пример 1 — видео На YouTube

YouTube предлагает возможность встраить видео на веб-страницах. С помощью простой веб-страницы забоя это легко показать в модуле задач:

![Видео YouTube](~/assets/images/task-module/youtube-example.png)

Вот HTML для этой страницы без CSS:

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

CSS выглядит так:

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

### <a name="example-2---powerapp"></a>Пример 2 . PowerApp

Такой же подход можно использовать и для встраить PowerApp. Поскольку высота и ширина каждого отдельного PowerApp настраиваются, может потребоваться изменить высоту и ширину, чтобы достичь желаемой презентации.

![PowerApp управления активами](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

И CSS:

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Адаптивная карта или вложение бот-карты адаптивной карты

Как мы уже отмечали выше, в зависимости от того, как вы назовете свою, вам потребуется использовать либо адаптивную карту, либо вложение бота-бота адаптивной карты (это всего лишь адаптивная карта, завернутая в объект `card` вложения).

При наводке со вкладки необходимо использовать адаптивную карточку. Вот очень простой пример:

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

При наложении на бота необходимо использовать вложение бота-бота адаптивной карты, как в примере ниже:

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

Вам необходимо помнить, является ли вы ссылкой на модуль задач, содержащий адаптивную карту от бота или вкладки.

## <a name="task-module-deep-link-syntax"></a>Синтаксис глубокой ссылки модуля задач

Глубокая ссылка модуля задач — это просто сериализация объекта [TaskInfo](#the-taskinfo-object) с двумя другими частями информации и `APP_ID` `BOT_APP_ID` необязательно:

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

См. [объект TaskInfo](#the-taskinfo-object) для типов данных и допустимых значений `<TaskInfo.url>` для , , , и `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` .

> [!TIP]
> Убедитесь, что URL-адрес кодирует глубокую ссылку, особенно при использовании параметра (например, функции `card` JavaScript). [ `encodeURI()` ](https://www.w3schools.com/jsref/jsref_encodeURI.asp)

Ниже данная `APP_ID` информация. `BOT_APP_ID`

| Значение | Тип | Обязательный? | Описание |
| --- | --- | --- | --- |
| `APP_ID` | string | Да | ID [приложения,](~/resources/schema/manifest-schema.md#id) на который выдают ссылку на модуль задач. Массив [validDomains в](~/resources/schema/manifest-schema.md#validdomains) манифесте для должен содержать домен, если `APP_ID` находится в `url` `url` URL-адресе. (ID приложения уже известен при вызове модуля задач со вкладки или бота, поэтому он не включен `TaskInfo` в .) |
| `BOT_APP_ID` | string | Нет | Если задано значение, объект отправляется через `completionBotId` `result` сообщение `task/submit invoke` указанному боту. `BOT_APP_ID` должно быть указано как бот в манифесте приложения, т. е. вы не можете просто отправить его любому боту. |

Обратите внимание, что он действителен для одного и того же и во многих случаях будет иметь бот, так как рекомендуется использовать его в качестве удостоверения приложения, если он `APP_ID` `BOT_APP_ID` есть.

## <a name="keyboard-and-accessibility-guidelines"></a>Рекомендации по клавиатуре и доступности

С помощью модулей задач на основе HTML/JavaScript вы несете ответственность за то, чтобы модуль задач вашего приложения можно было использовать с помощью клавиатуры. Программы чтения с экрана также зависят от возможности навигации с помощью клавиатуры. На практике это означает две вещи:

1. Использование атрибута [tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) в тегах HTML для управления элементами, которые могут быть сфокусированы и если/где он участвует в последовательной навигации клавиатуры (обычно с клавишами <kbd>Tab</kbd> и <kbd>Shift-Tab).</kbd>
2. Обработка <kbd>ключа Esc</kbd> в JavaScript для модуля задач. Вот пример кода, показывающий, как это сделать:

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams обеспечит правильную работу навигации по клавиатуре из заголовка модуля задач в HTML и наоборот.

## <a name="code-sample"></a>Пример кода
|**Пример имени** | **Описание** | **.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|Пример модуля задач (Bots-V4) | Примеры для создания модулей задач. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 
|Пример модуля задач (Tabs + Bots-V3) | Примеры для создания модулей задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a>См. также

* [Запрос разрешений устройства](../concepts/device-capabilities/native-device-permissions.md)
* [Интеграция возможностей мультимедиа](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Интеграция возможностей сканера QR или штрихкодов в Teams](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Интеграция возможностей расположения в Teams](../concepts/device-capabilities/location-capability.md)
