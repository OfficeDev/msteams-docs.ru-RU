---
title: Определение команд поиска расширения обмена сообщениями
author: surbhigupta
description: Определение команд поиска расширения обмена сообщениями для Microsoft Teams приложений.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: none
ms.openlocfilehash: aaea89aa14e556dfa00e81e8ec72fe5fb4bbe744
ms.sourcegitcommit: 781e7b82240075e9d1f55e97f3f1dcbba82a5e4d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2021
ms.locfileid: "60566367"
---
# <a name="define-messaging-extension-search-commands"></a>Определение команд поиска расширения обмена сообщениями

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Команды поиска расширения обмена сообщениями позволяют пользователям искать внешние системы и вставлять результаты этого поиска в сообщение в виде карточки. В этом документе приводятся руководства по выбору расположения ссылок команды поиска и добавлению команды поиска в манифест приложения.

> [!NOTE]
> Ограничение размера карты результатов — 28 КБ. Карта не отправляется, если ее размер превышает 28 КБ.

## <a name="select-search-command-invoke-locations"></a>Выберите расположения команд поиска, вызываемой

Команда поиска вызывается из любого из следующих местоположений:

* Область составить сообщение. Кнопки в нижней части области составить сообщение.
* Командная шкатулка: @mentioning в командном окне.

  При вызове команды поиска из области составить сообщение пользователь отправляет результаты в беседу. Когда он вызывается из командного окна, пользователь взаимодействует с результативной картой или копирует ее для использования в другом месте.

На следующем изображении отображаются расположения ссылок команды поиска:

![Команда поиска вызывает расположения](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## <a name="add-the-search-command-to-your-app-manifest"></a>Добавление команды поиска в манифест приложения

Чтобы добавить команду поиска в манифест приложения, необходимо добавить новый объект на верхний уровень `composeExtension` манифеста приложения JSON. Вы можете добавить команду поиска либо с помощью App Studio, либо вручную.

### <a name="create-a-search-command"></a>Создание команды поиска 

Вы можете создать команду поиска с помощью ** App Studio** или **портала разработчика.**

> [!NOTE]
>  App Studio скоро будет отвягот. Настройка, распространение и управление Teams приложениями с помощью нового [портала разработчиков.](https://dev.teams.microsoft.com/)

# <a name="app-studio"></a>[App Studio](#tab/AS)

> [!NOTE]
> Обязательным условием для создания команды поиска является то, что вы уже должны создать расширение обмена сообщениями. Сведения о создании расширения обмена сообщениями см. в сообщении о создании расширения [обмена сообщениями.](~/messaging-extensions/how-to/create-messaging-extension.md)

**Создание команды поиска**

1. Откройте **App Studio** Microsoft Teams клиента и выберите вкладку Редактор **Манифеста.**
1.  Если вы уже создали пакет приложений в **App Studio,** выберите из списка. Если вы не создали пакет приложений, импортировать существующий пакет.
1. После импорта пакета приложений выберите **расширения обмена сообщениями** в статье **Capabilities.** Вы получите всплывающее окно, чтобы настроить расширение обмена сообщениями.
1. Выберите **Настройка в** окне, чтобы включить расширение обмена сообщениями в приложение. На следующем изображении отображается страница расширения обмена сообщениями: 

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. Для создания расширения обмена сообщениями необходим зарегистрированный бот Майкрософт. Можно использовать существующий бот или создать новый бот. Выберите **создание нового варианта бота,** назови имя нового бота и выберите **Create**. На следующем изображении отображается создание бота для расширения обмена сообщениями:

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. Выберите **Добавить** в **разделе Команда** страницы расширения обмена сообщениями, чтобы включить команды, которые решают поведение расширения обмена сообщениями.   
На следующем изображении отображается добавление команд для расширения обмена сообщениями:

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. Выберите **Разрешить пользователям запрашивать у службы сведения и вставить их в сообщение.** На следующем изображении отображается выбор параметров команды поиска:

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. Добавление **командного и** **заголовок**.
1. Выберите расположение, на котором должна вызываться команда поиска. Выбор сообщения **в** настоящее время не изменяет поведение команды поиска. На следующем изображении отображается расположение вызова команды поиска:

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. Добавьте параметр поиска и выберите **Сохранить**.

# <a name="developer-portal"></a>[Портал разработчика](#tab/DP)

**Создание команды поиска с помощью портала разработчика**

1. Перейдите на **[портал Разработчик](https://dev.teams.microsoft.com/)**.
    
   <img src="~/assets/images/tdp/tdp_home_1.png" alt="Screenshot of TDP" width="500"/>
    
1. Перейдите к **приложениям.**
    
    <img width="500px" alt="Screenshot of TDP Open" src="~/assets/images/tdp/screen2.png"/>
    
1. Если вы уже создали пакет приложений на **портале разработчиков,** выберите его из списка. Если вы не создали пакет приложений, выберите **Импорт существующего приложения.**

    <img width="500px" alt="Screenshot of import app in tdp" src="~/assets/images/tdp/screen3.png"/>

1. Перейдите к **функциям Приложения.**  

    <img width="500px" alt="TDP messaging extension" src="~/assets/images/tdp/tdp-me.png"/>

1. Выберите **расширения обмена сообщениями из** **функций Приложения.** Всплывающее окно, как представляется, настроено расширение обмена сообщениями.
    
   <img width="500px" alt="TDP messaging extension set up" src="~/assets/images/tdp/tdp-app-me.png"/>

1. Выберите **бот расширения сообщений** из списка drop down в **ID** расширений сообщений и выберите **Сохранить**.

    <img width="500px" alt="TDP messaging extension bot" src="~/assets/images/tdp/tdp-me-bot.png"/>

1. Выберите **Добавить команду**. Всплывающее окно добавляет команду.

    <img width="500px" alt="TDP messaging extension command" src="~/assets/images/tdp/tdp-me-add-command.png"/>

1. Выберите **команду поиска и** введите поля команд.

    <img width="500px" alt="TDP messaging extension search command" src="~/assets/images/tdp/tdp-me-search-command.png"/>

1. Введите поля параметров и выберите **Сохранить**.

    <img width="500px" alt="TDP messaging extension search parameter" src="~/assets/images/tdp/tdp-me-search-parameter.png"/>

---


### <a name="create-a-search-command-manually"></a>Создание команды поиска вручную 

Чтобы вручную добавить команду поиска расширения обмена сообщениями в манифест приложения, необходимо добавить в массив объектов следующие `composeExtension.commands` параметры:

| Имя свойства | Назначение | Обязательный? | Минимальная версия манифеста |
|---|---|---|---|
| `id` | Это свойство — уникальный ID, который назначается команде поиска. Запрос пользователя включает этот ID. | Да | 1.0 |
| `title` | Это свойство — командное имя. Это значение отображается в пользовательском интерфейсе (пользовательском интерфейсе). | Да | 1.0 |
| `description` | Это свойство — текст справки, указывающий, что делает эта команда. Это значение отображается в пользовательском интерфейсе. | Да | 1.0 |
| `type` | Это свойство должно быть `query` . | Нет | 1.4 |
|`initialRun` | Если это свойство заданной для **true,** это указывает на то, что эта команда должна быть выполнена, как только пользователь выберет эту команду в пользовательском интерфейсе. | Нет | 1.0 |
| `context` | Это свойство — необязательный массив значений, определяя контекст, в котором доступно действие поиска. Возможные значения — `message`, `compose` и `commandBox`. Значение по умолчанию: `["compose", "commandBox"]`. | Нет | 1.5 |

Необходимо добавить сведения о параметре поиска, который определяет текст, видимый пользователю в Teams клиенте.

| Имя свойства | Назначение | Требуется? | Минимальная версия манифеста |
|---|---|---|---|
| `parameters` | Это свойство определяет статический список параметров для команды. | Нет | 1.0 |
| `parameter.name` | Это свойство описывает имя параметра. Это отправляется в службу в запросе пользователя. | Да | 1.0 |
| `parameter.description` | Это свойство описывает цели параметра или пример необходимого значения. Это значение отображается в пользовательском интерфейсе. | Да | 1.0 |
| `parameter.title` | Это свойство — короткое удобное название параметра или метка. | Да | 1.0 |
| `parameter.inputType` | Это свойство задалось типу требуемого ввода. Возможные `text` значения: `textarea` , , , , `number` `date` `time` `toggle` . По умолчанию `text` установлено значение . | Нет | 1.4 |

#### <a name="example"></a>Пример

В следующем разделе приводится пример простого манифеста приложения объекта, определяющий `composeExtensions` команду поиска: 

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}
```
Полный манифест приложения см. в [схеме манифеста Приложения.](~/resources/schema/manifest-schema.md)

## <a name="code-sample"></a>Пример кода

| Имя образца           | Описание | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Teams расширения обмена сообщениями| Описывает, как определить команды действий, создать модуль задач и реагировать на отправку действия модуля задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams расширения обмена сообщениями   |  Описывает, как определить команды поиска и реагировать на поиски.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Откликайся на команды поиска.](~/messaging-extensions/how-to/search-commands/respond-to-search.md)

