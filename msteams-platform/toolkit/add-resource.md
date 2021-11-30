---
title: Добавление ресурсов в Teams приложения
author: MuyangAmigo
description: Описывает добавление ресурсов Teams набор средств
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: dcaa4475db62be2cebbbe2b1b74e0bbbd7fb5398
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227758"
---
# <a name="add-cloud-resources-to-your-teams-app"></a>Добавление облачных ресурсов в Teams приложение

TeamsFx помогает в предоставлении облачных ресурсов для размещения приложений. Кроме того, можно дополнительно добавить облачные ресурсы, которые подходят для разработки.

## <a name="prerequisite"></a>Предварительное условие

* [Установка Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии v3.0.0+.

> [!TIP]
> У вас уже должен быть проект Teams приложения.

## <a name="add-cloud-resources-using-teams-toolkit"></a>Добавление облачных ресурсов с Teams набор средств

> [!IMPORTANT]
> Необходимо уложить каждую среду после добавления ресурса.

1. Откройте **Visual Studio Code**.
1. Выберите **Teams набор средств** левой панели:

    ![Активация Teams набор средств](./images/activate-teams-toolkit.png)

1. В панели Teams набор средств панели выберите **Добавить облачные ресурсы:**

    ![Добавление облачных ресурсов](./images/add-cloud-resources.png)

    Вы также можете открыть палитру команд и ввести **Teams: Добавить облачные ресурсы:**
    
    > [!NOTE]
    > Следуйте за тем же процессом, что и при запуске из Tree View:

    ![Альтернативные облачные ресурсы](./images/alternate-cloud-resources.png)

1. Во всплывающее приложение выберите любые облачные ресурсы, которые необходимо добавить в проект Teams приложения:

     ![Выбор облачных ресурсов](./images/select-cloud-resources.png)

1. Нажмите кнопку **ОК**.

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>Добавление облачных ресурсов с помощью CLI TeamsFx в командном окне

1. Изменение каталога в **каталог проекта.**
1. Выполните команду, чтобы добавить различные возможности.

В следующей таблице описываются облачные ресурсы и соответствующие команды для их добавления:

|Облачные ресурсы|Команда|
|---------------|----------|
| Функция Azure|`teamsfx resource add azure-function --function-name your-func-name`|
| База данных Azure SQL|`teamsfx resource add --function-name your-func-name`|
| Управление API Azure|`teamsfx resource add azure-apim`|

## <a name="what-cloud-resources-can-be-added"></a>Какие облачные ресурсы можно добавить

TeamsFx обеспечивает бесшовную интеграцию с службами Azure, которые являются общими для следующих сценариев приложений:

- [Функции Azure:](/azure/azure-functions/functions-overview)решение без серверов для удовлетворения требований по запросу, например создание веб-API для Teams приложений.
- [База SQL Azure](/azure/azure-sql/database/sql-database-paas-overview): полностью управляемой платформы в качестве двигателя базы данных службы (PaaS), чтобы служить в качестве Teams хранения данных приложений.
- [Управление API](/azure/azure-sql/database/sql-database-paas-overview)Azure: шлюз API, который можно использовать для администрирования API, созданных для Teams приложений, и публикации их для использования в других приложениях, например Power Apps.

## <a name="what-happens-when-you-add-resources"></a>Что происходит при добавлении ресурсов

При добавлении ресурсов в проект будут внесены следующие изменения:

- В Azure.parameter могут быть добавлены новые параметры. {env}.json для предоставления необходимых сведений для предоставления.
- Новое содержимое добавляется в ARM в папке (кроме файлов в папке) для `templates/azure` `templates/azure/teamsfx` создания добавленных ресурсов Azure.
- Файлы в папке регенерированы, чтобы убедиться, что необходимая конфигурация TeamsFx является новой для добавленных `templates/azure/teamsfx` ресурсов Azure.
- `.fx/projectSettings.json` обновляется для отслеживания ресурсов, присутствующих в проекте.

В то же время для каждого типа ресурса есть некоторые дополнительные изменения:

|Добавлены ресурсы|Что изменилось|Почему внесены эти изменения|
|---------------|---------------|-----------------------------|
|Функции Azure|Код шаблона Azure Functions добавляется в подмостки с пути `yourProjectFolder/api`</br></br>`launch.json` и `task.json` обновляется в `.vscode` папке.| Включите шаблон триггера hello world http в проект.</br></br> Чтобы включить необходимые сценарии для Visual Studio Code, которые необходимо отключить приложение локально.|
|Управление API Azure|Файл спецификации Открытого API, добавленный в подмостки с пути `yourProjectFolder/openapi`|Это файл спецификации API, определяющий API после публикации.|

## <a name="limitations"></a>Ограничения

- В проект можно добавить только одно приложение функции База данных SQL Azure/AIM-службу.
- Нельзя добавлять ресурсы, если в проекте не содержится приложение вкладки.

## <a name="see-also"></a>См. также

> [!div class="nextstepaction"]
> [Предоставление облачных ресурсов](provision.md)
