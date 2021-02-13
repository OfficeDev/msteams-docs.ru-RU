---
title: Что такое модули задач?
author: clearab
description: Добавление модальных всплывающих экранов для сбора или отображения сведений о приложениях Microsoft Teams для пользователей.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d92da7e6def6d66efd2f94600b7b8f8847553701
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231661"
---
# <a name="what-are-task-modules"></a>Что такое модули задач?

Модули задач позволяют создавать модальные всплывающие блоки в приложении Teams. Во всплывающее представление можно запустить собственный код HTML или JavaScript, отобразить мини-приложения на основе youTube или Microsoft Stream или показать адаптивную `<iframe>` [карточку.](/adaptive-cards/) Они особенно полезны для инициирования и выполнения задач или отображения подробной информации, например видео или панелей мониторинга Power BI. Всплывающие чаты часто более естественны для пользователей, которые инициируются и завершают задачи, по сравнению с вкладками или ботами на основе бесед.

Модули задач на основе вкладок Microsoft Teams; По сути, они являются вкладками во всплывающее окно. Они используют тот же SDK, поэтому если вы создали вкладку, вы уже на 90 % можете создать модуль задач.

Модули задач могут вызываться тремя способами:

* **Канал или личные вкладки.** С помощью SDK вкладок Microsoft Teams можно вызывать модули задач из кнопок, ссылок или меню на вкладке. Это подробно [освещается здесь.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **Боты.** Кнопки на [карточках, отправленных](~/task-modules-and-cards/cards/cards-reference.md) ботом. Это особенно полезно, если вам не нужны все в канале, чтобы увидеть, что вы делаете с ботом. Например, когда пользователи отвечают на опрос в канале, не очень полезно видеть запись о том, что опрос создается. [Это подробно освещается здесь.](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **За пределами Teams по прямой ссылке.** Вы также можете создавать URL-адреса для вызова модуля задачи из любого места. [Это подробно освещается здесь.](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a>Как выглядит модуль задачи

Вот как выглядит модуль задачи при вызове из бота (без цветных прямоугольников и нумитных кругов, конечно):

![Пример модуля задач](~/assets/images/task-module/task-module-example.png)

Рассмотрим его.

1. Значок вашего [ `color` приложения.](~/resources/schema/manifest-schema.md#icons)
2. Имя вашего [ `short` приложения.](~/resources/schema/manifest-schema.md#name)
3. Заголовок модуля задачи, указанный в свойстве объекта `title` [TaskInfo.](#the-taskinfo-object)
4. Кнопка закрытия или отмены модуля задачи. Если пользователь нажал эту кнопку, ваше приложение получит `err` событие, как [описано здесь.](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module) (**Примечание.** В настоящее время невозможно обнаружить это событие, когда модуль задачи вызывается ботом.)
5. Синий прямоугольник — это то место, где отображается веб-страница при загрузке собственной веб-страницы с помощью свойства `url` [объекта TaskInfo.](#the-taskinfo-object) Дополнительные подробности см. в [разделе "Размер модуля задачи"](#task-module-sizing) ниже.
6. Если вы отображаете адаптивную карточку с помощью свойства объекта `card` [TaskInfo,](#the-taskinfo-object) заполнение будет добавлено для вас, в противном случае вам придется обработать [это самостоятельно.](#task-module-css-for-htmljavascript-task-modules)
7. Здесь будут отрисовываться кнопки адаптивной карточки. Если вы используете собственную страницу, необходимо создать собственные кнопки.

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>Общие сведения о том, как сдуть и отклонять модули задач

Модули задач могут вызываться из вкладок, ботов или глубоких ссылок, и в одном из них могут быть HTML-коды или адаптивные карточки, поэтому существует много гибкости с точки зрения того, как они вызываются и как работать с результатом взаимодействия пользователя. В приведенной ниже таблице приведена итоговая по этим процессу работа.

| **Вызывается через...** | **Модуль задачи — HTML/JavaScript** | **Модуль задачи — это адаптивная карточка** |
| --- | --- | --- |
| **JavaScript на вкладке** | 1. Использование функции SDK клиента Teams `tasks.startTask()` с необязательной функцией `submitHandler(err, result)` вызова <br/><br/> 2. После завершения работы пользователя в коде модуля задачи вызовите функцию Teams SDK с объектом в `tasks.submitTask()` `result` качестве параметра. Если в `submitHandler` параметре указан параметр callback, Teams вызывает его `tasks.startTask()` в качестве `result` параметра.<br/><br/> 3. Если при подавке произошла ошибка, функция будет вызвана `tasks.startTask()` `submitHandler` со `err` строкой. <br/><br/> 4. Вы также можете указать a при вызове — в этом `completionBotId` `teams.startTask()` случае `result` отправляется боту. | 1. Вызовите функцию SDK клиента Teams с объектом TaskInfo и содержащей JSON для адаптивной карточки, которая будет отражаться во всплывающее представление `tasks.startTask()` модуля [](#the-taskinfo-object) `TaskInfo.card` задачи. <br/><br/> 2. Если в методе callback указан метод, Teams вызывает его со строкой, если при вызове произошла ошибка или пользователь закрывает всплывающее сообщение модуля задачи с помощью `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` X в правом верхнем. <br/><br/> 3. Если пользователь нажал кнопку Action.Submit, его объект возвращается `data` в качестве значения `result` . |
| **Кнопка карточки бота** | 1. Кнопки карточки бота в зависимости от типа кнопки могут вызывать модули задач двумя способами: URL-адресом глубокой ссылки или отправкой `task/fetch` сообщения. См. ниже, как работают URL-адреса глубоких ссылок. <br/><br/> 2. Если действие кнопки ( тип кнопки для адаптивных карточек), боту отправляется событие (HTTP POST под обложками), и бот отвечает на ЗАПРОС POST с http 200 и тело ответа, содержащее оболочку вокруг объекта `type` `task/fetch` `Action.Submit` `task/fetch invoke` [TaskInfo.](#the-taskinfo-object) Это подробно объясняется при извлечении модуля задачи [через задачу/извлечение.](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch)<br/><br/> 3. Teams отображает модуль задачи; Когда пользователь завершит работу, вызовите функцию Teams SDK с `tasks.submitTask()` `result` объектом в качестве параметра. <br/><br/> 4. Бот получает сообщение `task/submit invoke` с `result` объектом. У вас есть три различных способа ответа на сообщение: ничего не делать (задача успешно завершена), отображая сообщение пользователю во всплывающее окно или путем запроса другого окна модуля задачи (то есть создания мастера, как `task/submit` интерфейс). Эти три варианта более подробно обсуждаются в подробном обсуждении [задачи/отправки.](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit) | 1. Как и кнопки на карточках Bot Framework, кнопки на адаптивных карточках поддерживают два способа вызова модулей задач: URL-адреса с прямой связью с кнопками и с помощью `Action.openUrl` `task/fetch` `Action.Submit` кнопок. <br/><br/> 2. Модули задач с адаптивными карточками работают очень аналогично примеру HTML или JavaScript (см. слева). Главное отличие заключается в том, что так как при использовании адаптивных карт нет кода JavaScript, нельзя вызывать `tasks.submitTask()` . Вместо этого Teams берет объект и возвращает его в качестве полезной нагрузки события, как `data` `Action.Submit` `task/submit` [описано здесь.](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit) |
| **URL-адрес глубокой ссылки** <br/>[синтаксис URL-адреса](#task-module-deep-link-syntax) | 1. Teams вызывает модуль задачи; URL-адрес, который отображается внутри `<iframe>` указанного в `url` параметре глубокой ссылки. Не существует никакого `submitHandler` вызова. <br/><br/> 2. В JavaScript страницы в модуле задачи вызовите, чтобы закрыть его с помощью объекта в качестве параметра, так же, как при вызове с вкладки или кнопки карточки `tasks.submitTask()` `result` бота. Логика завершения немного отличается. Если логика завершения находится на клиенте (то есть если бота нет), то не будет никакого вызова, поэтому любая логика завершения должна находиться в коде перед `submitHandler` `tasks.submitTask()` вызовом. Об ошибках вызовов сообщается только через консоль. Если у вас есть бот, вы можете указать параметр в глубокой ссылке, чтобы `completionBotId` отправить `result` объект через `task/submit` событие. | 1. Teams вызывает модуль задачи; Тело карточки JSON адаптивной карточки указывается в качестве значения параметра глубокой ссылки в кодированном `card` URL-адресе. <br/><br/> 2. Пользователь закрывает модуль задачи, щелкнув X в верхней правой части модуля задачи или нажав кнопку `Action.Submit` на карточке. Так как вызовов нет, необходимо иметь бота для отправки значения полей `submitHandler` адаптивной карточки. Параметр в глубокой ссылке используется для указания бота для отправки данных `completionBotId` через `task/submit invoke` событие. |

> [!NOTE]
> На мобильных устройствах не поддерживается искомый модуль задачи из JavaScript.

## <a name="the-taskinfo-object"></a>Объект TaskInfo

Объект `TaskInfo` содержит метаданные для модуля задачи. Определение объекта приведено ниже. Необходимо **определить** либо `url` (для внедренного iFrame), либо `card` (для адаптивной карточки).

| Атрибут | Тип | Описание |
| --- | --- | --- |
| `title` | string | Отображается под именем приложения и справа от значка приложения |
| `height` | number или string | Это может быть число, представляющее высоту модуля задачи в пикселях, или `small` `medium` , или `large` . [Подробнее об обработке высоты и ширины см. ниже.](#task-module-sizing) |
| `width` | number или string | Это может быть число, представляющее ширину модуля задачи в пикселях, или `small` `medium` , или `large` . [Подробнее об обработке высоты и ширины см. ниже.](#task-module-sizing) |
| `url` | string | URL-адрес страницы, загруженной в модуле `<iframe>` задачи. Домен URL-адреса должен быть в массиве допустимого домена приложения [в](~/resources/schema/manifest-schema.md#validdomains) манифесте приложения. |
| `card` | Адаптивная карточка или вложение бота адаптивной карточки | JSON для адаптивной карточки, которая будет отображаться в модуле задачи. Если вы используете бота, необходимо использовать JSON адаптивной карточки в объекте Bot `attachment` Framework. На вкладке вы будете использовать только адаптивную карточку. [Вот пример.](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | Если клиент не поддерживает функцию модуля задачи, этот URL-адрес открывается на вкладке браузера. |
| `completionBotId` | string | Указывает ИД приложения-бота, в который отправляется результат взаимодействия пользователя с модулем задачи. Если этот объект задан, бот получит событие с объектом JSON в полезной нагрузке `task/submit invoke` события. |

> [!NOTE]
> Для функции модуля задачи необходимо, чтобы домены всех URL-адресов, которые вы хотите загрузить, были включены в массив `validDomains` манифеста приложения.

## <a name="task-module-sizing"></a>Размер модуля задачи

Использование в пикселях высоты и ширины с помощью `TaskInfo.width` integers. `TaskInfo.height` Однако в зависимости от размера окна команды и разрешения экрана они будут уменьшаться пропорционально при сохранении пропорций (ширина и высота).

Если и есть, либо размер красного прямоугольника на рисунке выше является пропорцией доступного `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` пространства: 20%, 50 %, 60 % для и `width` 20%, 50 %, 66% для `height` .

Модули задач, вызываемые с вкладки, можно динамически реаклизовать. После вызова можно вызвать, где свойства высоты и ширины объекта newSize соответствуют спецификации `tasks.startTask()` `tasks.updateTask(newSize)` TaskInfo (например. `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>CSS модуля задач для модулей задач HTML и JavaScript

Модули задач на основе HTML и JavaScript имеют доступ ко всей области модуля задачи под заголовщиком. Хотя это обеспечивает большую гибкость, если вы хотите, чтобы заполнение по краям было согласовано с элементами header и избегало лишних прокруток, необходимо предоставить правильный CSS. Вот несколько примеров использования.

### <a name="example-1---youtube-video"></a>Пример 1. Видео youTube

YouTube предлагает возможность встраить видео на веб-страницы. С помощью простой веб-страницы загона ее легко отдемонстрировать в модуле задачи:

![Видео с YouTube](~/assets/images/task-module/youtube-example.png)

Вот HTML-код для этой страницы без CSS:

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

### <a name="example-2---powerapp"></a>Пример 2. PowerApp

Такой же подход можно использовать и для встраивки PowerApp. Так как высота и ширина любого отдельного powerApp можно настраивать, вам может потребоваться изменить высоту и ширину для достижения нужного представления.

![PowerApp для управления активами](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

CSS::

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Адаптивная карточка или вложение карточки бота адаптивной карточки

Как мы уже отмечалось выше, в зависимости от того, как вы используете вашу, вам потребуется использовать либо адаптивную карту, либо вложение карточки бота адаптивной карточки (которая является просто адаптивной картой, упакованной в объект `card` вложения).

Когда вы используете вкладку, вам потребуется использовать адаптивную карточку. Вот очень простой пример:

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

При вложении бота вам потребуется использовать вложение карточки бота адаптивной карточки, как в примере ниже:

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

Необходимо помнить, что вы искомый модуль задачи, содержащий адаптивную карточку из бота или вкладки.

## <a name="task-module-deep-link-syntax"></a>Синтаксис глубокой ссылки модуля задачи

Глубокая ссылка модуля задачи — это просто сериализация объекта [TaskInfo](#the-taskinfo-object) с двумя другими частями информации и, при желании, `APP_ID` `BOT_APP_ID` :

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

См. [объект TaskInfo](#the-taskinfo-object) для типов данных и допустимых значений для `<TaskInfo.url>` , , , и `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` .

> [!TIP]
> Убедитесь, что URL-адрес кодирует глубокую ссылку, особенно при использовании параметра `card` (например, [ `encodeURI()` ](https://www.w3schools.com/jsref/jsref_encodeURI.asp)функции JavaScript).

Ниже данная информация и: `APP_ID` `BOT_APP_ID`

| Значение | Тип | Обязательный? | Описание |
| --- | --- | --- | --- |
| `APP_ID` | string | Да | ИД [приложения,](~/resources/schema/manifest-schema.md#id) которое выдает модуль задачи. Массив [validDomains в](~/resources/schema/manifest-schema.md#validdomains) манифесте должен содержать `APP_ID` домен, для которых указан `url` `url` URL-адрес. (ИД приложения уже известен, когда модуль задачи вызывается с помощью вкладки или бота, поэтому он не включен в `TaskInfo` .) |
| `BOT_APP_ID` | string | Нет | Если задано значение, объект отправляется через `completionBotId` `result` сообщение `task/submit invoke` указанному боту. `BOT_APP_ID` должен быть указан как бот в манифесте приложения, т. е. вы не можете просто отправить его любому боту. |

Обратите внимание, что это допустимо и должно быть одинаковым, и во многих случаях это будет, если приложение имеет бота, так как рекомендуется использовать его в качестве ИД приложения, если он `APP_ID` `BOT_APP_ID` существует.

## <a name="keyboard-and-accessibility-guidelines"></a>Рекомендации по клавиатуре и специальным возможности

С помощью модулей задач на основе HTML и JavaScript вы несете ответственность за то, чтобы модуль задач вашего приложения можно было использовать с клавиатурой. Программы чтения с экрана также зависят от возможности навигации с помощью клавиатуры. На практике это означает две вещи:

1. Использование атрибута [tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) в HTML-тегах для управления тем, какие элементы могут быть сфокусированы и если/где он участвует в последовательной навигации с помощью клавиатуры (обычно с клавишами <kbd>TAB</kbd> и <kbd>SHIFT-TAB).</kbd>
2. Обработка <kbd>клавиши ESC</kbd> в JavaScript для модуля задачи. Вот пример кода, показывающий, как это сделать:

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams обеспечит правильную работу навигации с помощью клавиатуры из заголовка модуля задачи в HTML и наоборот.

## <a name="task-module-samples"></a>Примеры модулей задач

* [Node.js/TypeScript](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs)
* [Пример C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp)

> [!div class="nextstepaction"]
> [Подробнее: запрос разрешений устройства](../concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
> [Подробнее: интеграция возможностей мультимедиа](../concepts/device-capabilities/mobile-camera-image-permissions.md)
