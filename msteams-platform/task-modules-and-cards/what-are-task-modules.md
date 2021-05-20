---
title: Что такое модули задач?
author: clearab
description: Добавление модальных всплывающих приложений для сбора или отображения информации пользователям из ваших Microsoft Teams приложений
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

Модули задач позволяют создавать модальные всплывающие окна в приложении Teams. Внутри всплывающего окна вы можете запустить свой собственный пользовательский HTML/ JavaScript `<iframe>` код, показать на основе виджета, таких как YouTube или Microsoft Stream видео или отображения [адаптивной карты](/adaptive-cards/). Они особенно полезны для инициирования и выполнения задач или отображения богатой информации, такой как видео или Power BI мониторинга. Всплывающее окно часто более естественно для пользователей, инициируя и выполняя задачи по сравнению с вкладкой или разговор на основе опыта бота.

Модули задач строятся на основе Microsoft Teams вкладок; они по существу вкладка внутри всплывающего окна. Они используют тот же SDK, так что если вы создали вкладку вы уже 90% пути к возможности создать модуль задач.

Модули задач можно вызывать тремя способами:

* **Канал или личные вкладки**: Использование Microsoft Teams Tabs SDK вы можете вызвать модули задач из кнопок, ссылок или меню на [вкладке. Это подробно описано здесь.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **Боты :** Кнопки на [картах, отправленных](~/task-modules-and-cards/cards/cards-reference.md) с вашего бота. Это особенно полезно, когда вам не нужно все в канале, чтобы увидеть, что вы делаете с ботом. Например, когда вам нужно собрать ответы пользователей на опрос в канале, нет никакой необходимости отображать пошаговые действия по созданию этого опроса.  [Это подробно описано здесь.](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **Вне Teams ссылки: Вы также можете** создавать URL-адреса для вызова модуля задач из любого места. [Это подробно описано здесь.](#task-module-deep-link-syntax)

## <a name="task-module-looks-like"></a>Модуль задачи выглядит как

Вот как выглядит модуль задач при вызовах бота (без цветных прямоугольников и проумереных кругов, конечно):

![Пример модуля задач](~/assets/images/task-module/task-module-example.png)

Давайте пройдите через него:

1. Значок вашего [ `color` приложения](~/resources/schema/manifest-schema.md#icons).
1. Имя вашего [ `short` приложения](~/resources/schema/manifest-schema.md#name).
1. Название модуля задачи указано в `title` свойстве объекта [TaskInfo.](#the-taskinfo-object)
1. Кнопка закрытия/отмены модуля задач. Если пользователь нажимает на это, ваше приложение получит событие, `err` описанное [здесь.](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)
    > [!Note]
    > В настоящее время невозможно обнаружить это событие при вызываемом модуле задачи от бота.
1. Синий прямоугольник является местом, где ваша веб-страница появляется, если вы загружаете свою собственную `url` веб-страницу, используя [свойство объекта TaskInfo.](#the-taskinfo-object) Более подробная информация приведена [в разделе размеров модуля задач](#task-module-sizing) ниже.
1. Если вы отображаете адаптивную карту `card` через свойство [объекта TaskInfo,](#the-taskinfo-object) обивка добавляется для вас, в противном случае вам нужно будет [справиться с этим самостоятельно.](#task-module-css-for-htmljavascript-task-modules)
1. Кнопки адаптивной карты будут отрисовывайте здесь. Если вы используете свою собственную страницу, вы должны создать свои собственные кнопки.

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>Обзор модулей задач вызова и увольнения

Модули задач могут быть вызваны из вкладок, ботов или глубоких ссылок, и то, что появляется в одном может быть либо HTML или адаптивной карты, так что есть много гибкости с точки зрения того, как они вызываются и как бороться с результатом взаимодействия пользователя. В таблице ниже кратко излагается, как это работает:

| **Вызывается через...** | **Модуль задач HTML/JavaScript** | **Модуль задачи - Адаптивная карта** |
| --- | --- | --- |
| **JavaScript во вкладке** | 1. Используйте функцию Teams SDK клиента с `tasks.startTask()` дополнительной `submitHandler(err, result)` функцией обратного вызова. <br/><br/> 2. В коде модуля задачи, когда пользователь закончен, позвоните Teams функцию SDK `tasks.submitTask()` с `result` объектом в качестве параметра. Если `submitHandler` обратный вызов был указан `tasks.startTask()` в, Teams называет его `result` в качестве параметра.<br/><br/> 3. Если была ошибка при вызове `tasks.startTask()` , функция `submitHandler` называется со строкой `err` вместо. <br/><br/> 4. Вы также можете указать `completionBotId` при вызове `teams.startTask()` - в этом `result` случае отправляется бот вместо. | 1. Позвоните Teams SDK с `tasks.startTask()` [объектом TaskInfo](#the-taskinfo-object) и `TaskInfo.card` содержащий JSON для адаптивной карты, чтобы показать в всплывающем модуле задачи. <br/><br/> 2. Если обратный вызов был указан в , Teams вызывает его со строкой, если была ошибка при `submitHandler` `tasks.startTask()` `err` вызове `tasks.startTask()` или если пользователь закрывает всплывающее окно модуля задачи с помощью X в правом верхнем. <br/><br/> 3. Если пользователь нажимает кнопку Action.Submit, `data` то его объект возвращается как значение `result` . |
| **Кнопка карты Бот** | 1. Кнопки карты Bot, в зависимости от типа кнопки, могут вызывать модули задач двумя способами: URL-адресом глубокой ссылки или отправкой `task/fetch` сообщения. Ниже приведены тем, как работают URL-адреса с глубокими ссылками. <br/><br/> 2. Если действие `type` кнопки `task/fetch` `Action.Submit` (тип кнопки для адаптивных карт), событие `task/fetch invoke` (HTTP POST под крышкой) отправляется боту, и бот реагирует на POST с HTTP 200 и органом реагирования, содержащим обертку вокруг [объекта TaskInfo.](#the-taskinfo-object) Это подробно объясняется [вызовом модуля задачи с помощью задачи/извлечения.](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-through-taskfetch)<br/><br/> 3. Teams отображает модуль задачи; когда пользователь закончит, позвоните в Teams функцию SDK `tasks.submitTask()` с `result` объектом в качестве параметра. <br/><br/> 4. Бот получает `task/submit invoke` сообщение, которое содержит `result` объект. У вас есть три различных способа ответа на `task/submit` сообщение: ничего не делать (задача успешно выполнена), отображая сообщение пользователю в всплывающем окне, или ссылаясь на другое окно модуля задач (т.е. создавая мастер-как опыт). Эти три варианта обсуждаются более [подробно в подробном обсуждении задачи / представить](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | 1. Как и кнопки на картах Bot Framework, кнопки на адаптивных картах поддерживают два способа вызова модулей задач: url-адреса с кнопками `Action.openUrl` и с `task/fetch` помощью `Action.Submit` кнопок. <br/><br/> 2. Модули задач с адаптивными картами работают очень похоже на html/JavaScript (см. слева). Основное различие заключается в том, что, поскольку при использовании адаптивных карт JavaScript нет, нет никакого способа `tasks.submitTask()` позвонить. Вместо Teams, вы `data` принимаете объект `Action.Submit` от и возвращает его в качестве полезной нагрузки в `task/submit` случае, как описано [здесь](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). |
| **Глубокая ссылка URL** <br/>[синтаксис URL-адреса](#task-module-deep-link-syntax) | 1. Teams вызывает модуль задачи; URL-адрес, который `<iframe>` отображается внутри указанного `url` параметра глубокой ссылки. Обратного вызова `submitHandler` нет. <br/><br/> 2. В JavaScript страницы в модуле задачи, вызов, чтобы закрыть его с объектом `tasks.submitTask()` `result` в качестве параметра, так же, как при вызове его из вкладки или кнопки карты бота. Однако логика завершения несколько иная. Если ваша логика завершения находится на клиенте (т.е. если нет бота) нет `submitHandler` обратного вызова, поэтому любая логика завершения должна быть в коде, предшествующем вызову `tasks.submitTask()` . Ошибки вызова сообщаются только через консоль. Если у вас есть бот, то вы можете `completionBotId` указать параметр в глубокой ссылке, чтобы `result` отправить объект через `task/submit` событие. | 1. Teams вызывает модуль задачи; Корпус карты JSON адаптивной карты указан как URL-закодированное значение `card` параметра глубокой ссылки. <br/><br/> 2. Пользователь закрывает модуль задачи, нажав на X в правом верхнем правом части модуля задачи или нажав `Action.Submit` кнопку на карте. Так как нет `submitHandler` вызова, вы должны иметь бота, чтобы отправить значение адаптивных полей карты. Вы используете `completionBotId` параметр в глубокой ссылке, чтобы указать бота для отправки данных через `task/submit invoke` событие. |

## <a name="the-taskinfo-object"></a>Объект TaskInfo

Объект `TaskInfo` содержит метаданные для модуля задач. Определение объекта приведено ниже. Вы **должны** определить либо `url` для встроенного iFrame или `card` для адаптивной карты.

| Атрибут | Тип | Описание |
| --- | --- | --- |
| `title` | string | Появляется под именем приложения и справа от значка приложения. |
| `height` | number или string | Это может быть число, представляющее высоту модуля задачи в пикселях, `small` `medium` или, `large` или. [Смотрите ниже, как высота и ширина обрабатываются.](#task-module-sizing) |
| `width` | number или string | Это может быть число, представляющее ширину модуля задачи в пикселях, `small` `medium` или, или `large` . [Смотрите ниже, как высота и ширина обрабатываются.](#task-module-sizing) |
| `url` | Строка | URL страницы, загруженный в качестве `<iframe>` внутреннего модуля задачи. Домен URL должен быть в массиве [приложения validDomains в](~/resources/schema/manifest-schema.md#validdomains) манифесте вашего приложения. |
| `card` | Адаптивная карта или вложение карты Adaptive card | JSON для адаптивной карты, чтобы появиться в модуле задачи. Если вы хотите получить вызов от бота, вам нужно будет использовать адаптивную карту JSON в объекте Bot `attachment` Framework. Из вкладки вы будете использовать только адаптивную карту. [Вот пример.](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | Строка | Если клиент не поддерживает функцию модуля задач, этот URL-адрес открыт во вкладке браузера. |
| `completionBotId` | Строка | Определяет идентификатор бота App ID для отправки результата взаимодействия пользователя с модулем задач. Если указано, бот получит событие `task/submit invoke` с объектом JSON в полезной нагрузке события. |

> [!NOTE]
> Функция модуля задач требует, чтобы домены любых URL-адресов, которые вы хотите загрузить, `validDomains` были включены в массив в манифесте вашего приложения.

## <a name="task-module-sizing"></a>Размер модуля задач

Использование интеграторов для `TaskInfo.width` и `TaskInfo.height` будет устанавливать высоту и ширину в пикселях. Однако в зависимости от размера окна группы и разрешения экрана они будут пропорционально уменьшены при сохранении соотношения сторон (ширина/высота).

Если `TaskInfo.width` `TaskInfo.height` и `"small"` `"medium"` есть, или размер красного `"large"` прямоугольника на картинке выше, доля от доступного пространства: 20%, 50%, 60% для `width` и 20%, 50%, 66% для `height` .

Модули задач, вызываемые из вкладки, могут быть динамически реилизированы. После вызова `tasks.startTask()` вы можете `tasks.updateTask(newSize)` позвонить, где высота и ширина свойства на newSize объект соответствует спецификации TaskInfo (например. `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>Модуль задач CSS для модулей задач HTML/JavaScript

Модули задач на основе HTML/JavaScript имеют доступ ко всей области модуля задач ниже заголовка. Хотя это обеспечивает большую гибкость, если вы хотите обивка по краям, чтобы выровнять с элементами заголовка и избежать ненужных scrollbars вам нужно обеспечить право CSS. Вот несколько примеров для нескольких случаев использования.

### <a name="example-1---youtube-video"></a>Пример 1 - видео YouTube

YouTube предлагает возможность встраивания видео на веб-страницах. Используя простую веб-страницу заглушки, это легко показать в модуле задач:

![Видео YouTube](~/assets/images/task-module/youtube-example.png)

Вот HTML для этой страницы, без CSS:

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

### <a name="example-2---powerapp"></a>Пример 2 - PowerApp

Вы также можете использовать тот же подход для встраивания PowerApp. Поскольку высота/ширина любого отдельного PowerApp настраивается, возможно, потребуется настроить высоту и ширину для достижения желаемой презентации.

![Управление активами PowerApp](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

И CSS является:

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Адаптивная карта или адаптивная карта бот-карты вложения

Как мы уже отмечали выше, в зависимости от того, как вы ссылаееся на вас вам `card` нужно будет использовать либо адаптивной карты, или адаптивной карты бот карты вложения (который является просто адаптивной карты, завернутые в объект вложения).

Когда вы вызове из вкладки, вам нужно будет использовать адаптивную карту. Вот очень простой пример:

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

Когда вы ссылаееся на бота, вам нужно будет использовать вложение карты adaptive card bot, как в приведеном ниже примере:

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

Вам нужно будет помнить, ссылаются ли вы на модуль задач, содержащий адаптивную карту от бота или вкладки.

## <a name="task-module-deep-link-syntax"></a>Модуль задачи глубокий синтаксис соединения

Глубокий модуль задачи - это просто сериализация объекта [TaskInfo с двумя](#the-taskinfo-object) другими частями информации, `APP_ID` и факультативно: `BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Смотрите [объект TaskInfo](#the-taskinfo-object) для типов данных и допустимых `<TaskInfo.url>` значений `<TaskInfo.card>` `<TaskInfo.height>` для, , , и `<TaskInfo.width>` `<TaskInfo.title>` .

> [!TIP]
> Обязательно url-адрес кодирует глубокую ссылку, особенно при `card` использовании параметра (например, функции [ `encodeURI()` JavaScript).](https://www.w3schools.com/jsref/jsref_encodeURI.asp)

Вот информация и `APP_ID` `BOT_APP_ID` :

| Значение | Тип | Обязательный? | Описание |
| --- | --- | --- | --- |
| `APP_ID` | string | Да | Идентификатор [приложения,](~/resources/schema/manifest-schema.md#id) ссылающегося на модуль задачи. Действительный [массивDomains в](~/resources/schema/manifest-schema.md#validdomains) манифесте для `APP_ID` должен содержать домен, `url` если находится в `url` URL. (Идентификатор приложения уже известен, когда модуль задачи вызывается из вкладки или бота, поэтому он не включен `TaskInfo` в .) |
| `BOT_APP_ID` | string | Нет | Если значение `completionBotId` для указанного, `result` объект отправляется через сообщение `task/submit invoke` указанному боту. `BOT_APP_ID` должны быть указаны в качестве бота в манифесте приложения, т.е. вы не можете просто отправить его любому боту. |

Обратите внимание, что он действителен и должен быть одинаковым, и во многих случаях `APP_ID` `BOT_APP_ID` будет, если приложение имеет бота, так как рекомендуется использовать его в качестве идентификатора приложения, если он есть.

## <a name="keyboard-and-accessibility-guidelines"></a>Рекомендации по клавиатуре и доступности

С помощью модулей задач на основе HTML/JavaScript вы несете ответственность за то, чтобы модуль задач вашего приложения можно было использовать с помощью клавиатуры. Программы чтения с экрана также зависят от способности ориентироваться с помощью клавиатуры. В практическом плане это означает две вещи:

1. Использование [атрибута tabindex в](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) HTML-тегах для управления элементами, которые могут быть сфокусированы и если/где он участвует в последовательной навигации клавиатуры (обычно <kbd>с ключами Tab</kbd> <kbd>и Shift-Tab).</kbd>
2. Обработка <kbd>ключа Esc</kbd> в JavaScript для модуля задач. Вот пример кода, показывающий, как это сделать:

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams гарантирует, что клавиатура навигации работает должным образом от заголовка модуля задачи в HTML и наоборот.

## <a name="code-sample"></a>Пример кода
|**Название образца** | **Описание** | **.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|Образец модуля задач (Bots-V4) | Образцы для создания модулей задач. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 
|Образец модуля задач (Tabs и Bots-V3) | Образцы для создания модулей задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a>См. также

* [Запрос разрешений устройства](../concepts/device-capabilities/native-device-permissions.md)
* [Интеграция возможностей мультимедиа](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Интеграция возможностей сканера qR или штрих-кодов в Teams](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Интеграция возможностей определения местоположения в Teams](../concepts/device-capabilities/location-capability.md)
