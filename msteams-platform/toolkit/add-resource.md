---
title: Добавление ресурсов в приложения Teams
author: MuyangAmigo
description: Описывает добавление ресурсов для набор средств Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 50cd3de693f70fd0c8414408bd6f4e6d3332d544
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2022
ms.locfileid: "65297207"
---
# <a name="add-cloud-resources-to-your-teams-app"></a>Добавление облачных ресурсов в приложение Teams

TeamsFx помогает подготавливать облачные ресурсы для размещения приложения. Вы также можете дополнительно добавить облачные ресурсы, соответствующие вашим потребностям в разработке.

## <a name="prerequisite"></a>Предварительное условие

[Установите набор средств Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) версии не ниже 3.0.0.

> [!TIP]
> Убедитесь, что у вас есть проект приложения Teams в Visual Studio Code.

## <a name="add-cloud-resources-using-teams-toolkit"></a>Добавление облачных ресурсов с помощью набор средств Teams

> [!IMPORTANT]
> После добавления ресурса необходимо подготовить каждую среду.

1. Откройте **Microsoft Visual Studio Code**.
1. На панели слева выберите **Набор средств Teams**.
1. На боковой панели набора средств Teams **Добавить облачные ресурсы**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add cloudresources.png" alt-text="Добавьте ресурсы":::

   Также можно открыть палитру команд и ввести **Teams: добавить облачные ресурсы**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addcloud.png" alt-text="добавить облачные ресурсы":::

1. Во всплывающем окне выберите облачные ресурсы, которые нужно добавить в проект приложения Teams:

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addresources.png" alt-text="добавить":::

1. Нажмите кнопку **ОК**.

Выбранные ресурсы успешно добавлены в ваш проект.

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>Добавление облачных ресурсов с помощью командной строки TeamsFx в командном окне

1. Измените каталог на **папку проекта**.
1. Выполните следующую команду, чтобы добавить в проект различные ресурсы:

|Облачный ресурс|Команда|
|---------------|----------|
| Функция Azure|`teamsfx resource add azure-function --function-name your-func-name`|
| База данных Azure SQL|`teamsfx resource add --function-name your-func-name`|
| Управление API Azure|`teamsfx resource add azure-apim`|
| Azure Key Vault|`teamsfx resource add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>Типы облачных ресурсов

TeamsFx интегрируется со службами Azure для следующих сценариев:

- [Функции Azure](/azure/azure-functions/functions-overview): бессерверное решение для удовлетворения требований по запросу, таких как создание веб-API для серверной части приложений Teams.
- [База данных SQL Azure](/azure/azure-sql/database/sql-database-paas-overview): ядро СУБД "платформа как услуга" (PaaS), которое служит хранилищем данных приложений Teams.
- [Управление API Azure](deploy.md). шлюз API, который можно использовать для администрирования API, созданных для приложений Teams, и их публикации для использования в других приложениях, например в приложениях Power.
- [Azure Key Vault](/azure/key-vault/general/overview): защита криптографических ключей и других паролей, используемых облачными приложениями и службами.

## <a name="add-cloud-resources"></a>Добавление облачных ресурсов

После добавления любого ресурса в проекте произойдут следующие изменения.

- В azure.parameter.{env}.json могут быть добавлены новые параметры, чтобы предоставить необходимую информацию для подготовки.
- Новое содержимое добавляется в шаблон ARM в папке `templates/azure`, за исключением файлов в папке `templates/azure/teamsfx` для создания добавленных ресурсов Azure.
- Файлы в папке `templates/azure/teamsfx` будут созданы повторно, чтобы обеспечить актуальность требуемой конфигурации TeamsFx для добавленных ресурсов Azure.
- `.fx/projectSettings.json` обновляется для отслеживания ресурсов, имеющихся в проекте.

После добавления ресурсов дополнительные изменения в вашем проекте выглядят следующим образом:

|Ресурсы|Изменения|Описание|
|---------------|---------------|-----------------------------|
|Функции Azure|Код шаблона функций Azure будет добавлен во вложенную папку с путем `yourProjectFolder/api`</br></br>`launch.json` и `task.json` будут обновлены в папке `.visual studio code`.| Включает в проект шаблон триггера HTTP hello world.</br></br> Включает необходимые сценарии для Visual Studio Code, которые должны выполняться при отладке приложения в локальном режиме.|
|Управление API Azure|Файл спецификации открытого API добавлен во вложенную папку с путем `yourProjectFolder/openapi`|Определяет ваш API после публикации, это файл спецификации API.|

## <a name="limitation"></a>Ограничение

Если проект вкладки создан на основе SPFx, добавление ресурсов будет невозможно.

## <a name="see-also"></a>См. также

[Подготовка облачных ресурсов](provision.md)
