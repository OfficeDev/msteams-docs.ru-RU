---
title: Добавление ресурсов в Teams приложения
author: MuyangAmigo
description: Описывает добавление ресурсов Teams набор средств
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 87420b5e2b133de32b8c27a4a8d34a90072a3c76
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435826"
---
# <a name="add-cloud-resources-to-your-teams-app"></a>Добавление облачных ресурсов в Teams приложение

TeamsFx помогает в предоставлении облачных ресурсов для размещения приложений. Кроме того, можно дополнительно добавить облачные ресурсы, которые подходят для разработки.

## <a name="prerequisite"></a>Предварительное условие

[Установка Teams набор средств](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии v3.0.0+.

> [!TIP]
> Убедитесь, что Teams приложения в Visual Studio Code.

## <a name="add-cloud-resources-using-teams-toolkit"></a>Добавление облачных ресурсов с Teams набор средств

> [!IMPORTANT]
> Необходимо уложить каждую среду после добавления ресурса.

1. Откройте **Microsoft Visual Studio код**.
1. Выберите **Teams набор средств** левой области.
1. В панели Teams набор средств панели выберите **Добавить облачные ресурсы**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add cloudresources.png" alt-text="Добавление ресурсов":::

   Вы также можете открыть палитру команд и ввести **Teams: Добавить облачные ресурсы**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addcloud.png" alt-text="добавление облачных ресурсов":::

1. Во всплывающее приложение выберите облачные ресурсы, которые необходимо добавить в проект Teams приложения:

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addresources.png" alt-text="добавление":::

1. Нажмите **OK**.

Выбранные ресурсы тщательно добавляются в проект.

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>Добавление облачных ресурсов с помощью CLI TeamsFx в окне команд

1. Изменение каталога в **каталог проекта**.
1. Выполните следующую команду, чтобы добавить в проект различные ресурсы:

|Облачный ресурс|Команда|
|---------------|----------|
| Функция Azure|`teamsfx resource add azure-function --function-name your-func-name`|
| База данных Azure SQL|`teamsfx resource add --function-name your-func-name`|
| Управление API Azure|`teamsfx resource add azure-apim`|
| Azure Key Vault|`teamsfx resource add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>Типы облачных ресурсов

TeamsFx интегрируется со службами Azure для следующих сценариев:

- [Функции Azure](/azure/azure-functions/functions-overview): решение без серверов для удовлетворения требований по запросу, например создание веб-API для Teams приложений.
- [База SQL Azure](/azure/azure-sql/database/sql-database-paas-overview): платформа в качестве двигателя базы данных службы (PaaS) для хранения данных Teams приложений.
- [Управление API](/azure/azure-sql/database/sql-database-paas-overview) Azure: шлюз API, который можно использовать для администрирования API, созданных для Teams приложений, и публикации их для использования в других приложениях, например в приложениях Power.
- [Хранилище ключей Azure](/azure/key-vault/general/overview): защита криптографических ключей и других секретов, используемых облачными приложениями и службами.

## <a name="add-cloud-resources"></a>Добавление облачных ресурсов

После добавления любого ресурса изменения в проекте будут следующими:

- В Azure.parameter могут быть добавлены новые параметры. {env}.json для предоставления необходимых сведений для предоставления.
- Новое содержимое добавляется к ARM в `templates/azure` `templates/azure/teamsfx` папке, за исключением файлов в папке для создания добавленных ресурсов Azure.
- Файлы в папке `templates/azure/teamsfx` регенерированы, чтобы убедиться, что необходимая конфигурация TeamsFx устарела для добавленных ресурсов Azure.
- `.fx/projectSettings.json` обновляется для отслеживания ресурсов, присутствующих в проекте.

После добавления resouces дополнительные изменения в проекте будут следующими:

|Ресурсы|Изменения|Описание|
|---------------|---------------|-----------------------------|
|Функции Azure|Код шаблона функций Azure добавляется в подмостки с пути `yourProjectFolder/api`</br></br>`launch.json` и `task.json` обновляется в папке `.visual studio code` .| Включает шаблон триггера hello world http в проект.</br></br> Включает необходимые сценарии для Visual Studio Code, которые необходимо выполнять при локальном отключе приложения.|
|Управление API Azure|Открытый файл спецификации API, добавленный в подмостки с пути `yourProjectFolder/openapi`|Определяет API после публикации, это файл спецификации API.|

## <a name="limitation"></a>Ограничение

Нельзя добавлять ресурсы, если вы создали проект SPFx вкладки.

## <a name="see-also"></a>См. также

[Подготовка облачных ресурсов](provision.md)
