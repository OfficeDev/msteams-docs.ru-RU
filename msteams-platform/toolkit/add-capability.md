---
title: Добавление возможностей в приложения Teams приложений
author: MuyangAmigo
description: Описание добавления возможностей Teams набор средств
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9d2e3d559bd9d561e3afae8b0db9544ab2ad86cc
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073533"
---
# <a name="add-capabilities-to-your-teams-apps"></a>Добавление возможностей в приложения Teams

Во время разработки приложения можно создать новое Teams с Teams приложения. В следующей таблице перечислены Teams приложения.

|**Возможность**|**Описание**|
|--------|-------------|
| Вкладки |  Вкладки — это простые HTML-теги, указывающие на домены, объявленные в манифесте приложения. Вкладки можно добавлять в составе канала внутри команды, группового чата или личного приложения для отдельного пользователя.|
| Боты |  Боты помогают взаимодействовать с веб-службой с помощью текстовых, интерактивных карточек и модулей задач|
| расширения для обмена сообщениями; | Расширения обмена сообщениями помогают взаимодействовать с веб-службой с помощью кнопок и форм в Microsoft Teams клиента|

## <a name="prerequisite"></a>Предварительное условие

* Установка [последней версии набора средств Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Убедитесь, что Teams открыт проект приложения в VS Code.

## <a name="limitations"></a>Ограничения

Ниже перечислены ограничения teamsFx при добавлении дополнительных возможностей.

* Можно добавить вкладки до 16 экземпляров
* Вы можете добавить бот и расширение для обмена сообщениями для одного экземпляра
## <a name="add-capabilities"></a>Добавление возможностей

> [!Note]
> После успешного добавления возможностей в приложение Teams подготовку для каждой среды.
* Вы можете добавить возможности с помощью Teams набор средств в Visual Studio Code
    1. Open **Microsoft Visual Studio Code**
    1. Выберите **Teams набор средств** панели слева
    1. Выбор **"Добавить возможности"**

        :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add capabilities.png" alt-text="capabilities":::

*   Вы также можете открыть палитру команд и ввести Teams: Add Capabilities:

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/tree view capabilities.png" alt-text="Альтернативные возможности":::


    1. Во всплывающем окне выберите возможности, которые необходимо включить в проект:

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select capabilities.png" alt-text="select":::

    2. Нажмите **кнопку "ОК"**

Выбранные возможности успешно добавлены в проект. В Teams набор средств создается исходный код для новых добавленных возможностей.

## <a name="add-capabilities-using-teamsfx-cli-in-command-window"></a>Добавление возможностей с помощью Командной строки TeamsFx в окне командной строки

1. Изменение каталога на **каталог проекта**
1. Выполните следующую команду, чтобы добавить в проект различные возможности:

   |Возможности и сценарии| Команда|
   |-----------------------|----------|
   |Добавление вкладки|`teamsfx capability add tab`|
   |Добавление бота|`teamsfx capability add bot`|
   |Добавление расширения для обмена сообщениями|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities"></a>Поддерживаемые возможности

Помимо возможностей, которые у Teams уже есть, вы можете добавить различные возможности в Teams приложения. В следующей таблице приведены различные Teams приложения.

|Существующие возможности|Другие поддерживаемые возможности|
|--------------------|--------------------|
|Вкладки с SPFx|Нет|
|Вкладки с Azure|Расширение бота и обмена сообщениями|
|Bot|Вкладки|
|Расширение для обмена сообщениями|Вкладки и бот|
|Вкладки и бот|Вкладки и расширение сообщений|
|Вкладки и расширение для обмена сообщениями|Вкладки и бот|
|Вкладки, бот и расширение для обмена сообщениями|Вкладки|
|Вкладки |Расширение бота и сообщения|

## <a name="add-bot-tab-and-messaging-extension"></a>Добавление бота, расширения табуляции и обмена сообщениями

После добавления бота и расширения для обмена сообщениями изменения в проекте будут следующими:

* Код шаблона бота добавляется во вложенную папку с путем `yourProjectFolder/bot`. Это включает шаблон приложения **hello world** bot в проект.
* `launch.json`и `task.json` в `.vscode` папке обновляются, что включает в себя необходимые скрипты для Visual Studio Code и выполняется при локальной отладке приложения.
* `manifest.template.json` file under `templates/appPackage` folder is updated, which includes the bot related information in the manifest file that represents your application in the Teams Platform. Внесены следующие изменения:
  * Идентификатор бота
  * Области бота
  * Команды, на которые может отвечать приложение-бот Hello World
* Обновляются указанные `templates/azure/teamsfx` ниже файлы, `templates/azure/provision/xxx`а bicep-файлы создаются повторно.
* Создаваемые файлы `.fx/config` повторно создаются, что гарантирует, что проект будет настроен с правильными конфигурациями для вновь добавленной возможности.

После добавления вкладки изменения в проекте будут следующими:

* Код шаблона интерфейсной вкладки добавляется во `yourProjectFolder/tab`вложенную папку с путем, который включает шаблон приложения вкладок **hello world** в проект
* `launch.json`и `task.json` в `.vscode` папке обновляются, что включает в себя необходимые скрипты для Visual Studio Code и выполняется при локальной отладке приложения.
* `manifest.template.json` file under `templates/appPackage` folder is updated, which includes tab-related information in the manifest file that represents your application in the Teams Platform. Изменения:
  * Настраиваемые и статические вкладки
  * Области вкладок
* Файлы в разделе `templates/azure/teamsfx` будут обновлены, `templates/azure/provision/xxx`и bicep-файл будет создан повторно.
* Файл в разделе `.fx/config` создается повторно, что гарантирует, что в проекте настроены правильные конфигурации для вновь добавленной возможности.



## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов](provision.md)
* [Создание нового Teams проекта](create-new-project.md)
