---
title: Добавление ресурсов в приложения Teams
author: MuyangAmigo
description: В этом модуле вы узнаете, как добавить ресурсы набора средств Teams, преимущества, ограничения и возможности
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: fc58610802a51af19efc32e579566fbf5e36feca
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616536"
---
# <a name="add-cloud-resources-to-microsoft-teams-app"></a>Добавление облачных ресурсов в приложение Microsoft Teams

Набор средств Teams помогает подготовить облачные ресурсы для размещения приложения. При необходимости можно добавить облачные ресурсы, которые соответствуют вашим потребностям разработки. Преимущество добавления дополнительных облачных ресурсов в TeamsFx заключается в том, что вы можете автоматически создавать все файлы конфигурации и подключаться к приложению Teams с помощью Набора средств Teams.

> [!NOTE]
> Если вы создали проект вкладки на основе SPFx, вы не сможете добавить облачные ресурсы Azure.

## <a name="add-cloud-resources"></a>Добавление облачных ресурсов

Добавить облачные ресурсы можно следующими способами:

### <a name="to-add-cloud-resources-by-using-teams-toolkit-in-visual-studio-code"></a>Добавление облачных ресурсов с помощью набора средств Teams в Visual Studio Code

   1. Откройте **Visual Studio Code**.
   1. Выберите **Набор средств Teams на** панели действий.
   1. Выберите **"Добавить компоненты"** в разделе **"РАЗРАБОТКА"**.

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/select-feature-updated.png" alt-text="Добавление функции из Набора средств Teams":::

### <a name="to-add-cloud-resources-by-using-command-palette"></a>Добавление облачных ресурсов с помощью палитры команд

   1. Выберите **"Просмотреть** > **палитру команд"...** или **CTRL+SHIFT+P**.

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/Teams-add-features.png" alt-text="Добавление функции из палитры команд":::

   1. **Введите Teams: добавление функций**.
   1. Нажмите клавишу **ВВОД**.

      :::image type="content" source="../assets/images/teams-toolkit-v2/manual/cloud/Teams-add-features1.png" alt-text="Введите добавление функции и введите":::

   1. Во всплывающем окне выберите **облачные ресурсы** , которые нужно добавить в проект.

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/updated-final-cloud.png" alt-text="Окончательный":::

  > [!NOTE]
  > После успешного добавления ресурса в приложение Teams необходимо подготовить каждую среду.

### <a name="add-cloud-resources-using-teamsfx-cli"></a>Добавление облачных ресурсов с помощью Командной строки TeamsFx

* Измените каталог на **папку проекта**.
* В следующей таблице перечислены возможности и необходимые команды:

  |Облачный ресурс|Команда|
  |---------------|----------|
  | Функция Azure|`teamsfx add azure-function`|
  | База данных Azure SQL|`teamsfx add azure-sql`|
  | Управление API Azure|`teamsfx add azure-apim`|
  | Azure Key Vault|`teamsfx add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>Типы облачных ресурсов

В следующих сценариях TeamsFx интегрируется со службами Azure:

* [Функции Azure](/azure/azure-functions/functions-overview): бессерверное решение для удовлетворения требований по запросу, таких как создание веб-API для серверной части приложений Teams.
* [База данных SQL Azure](/azure/azure-sql/database/sql-database-paas-overview): ядро СУБД "платформа как услуга" (PaaS), которое служит хранилищем данных приложений Teams.
* [Управление API Azure](deploy.md). Шлюз API можно использовать для администрирования API, созданных для приложений Teams, и их публикации для использования в других приложениях, таких как приложения Power.
* [Azure Key Vault](/azure/key-vault/general/overview): защита криптографических ключей и других паролей, используемых облачными приложениями и службами.

## <a name="changes-after-adding-cloud-resources"></a>Изменения после добавления облачных ресурсов

После добавления ресурсов в проект появляются следующие изменения:

* Новые параметры, добавленные в azure.parameter. {env}.json для предоставления необходимых сведений для подготовки.
* Новое содержимое включается в шаблон ARM `templates/azure`, за исключением того, `templates/azure/teamsfx` что файлы находятся в папке для добавления ресурсов Azure.
* Файлы в папке `templates/azure/teamsfx` будут созданы повторно, чтобы обеспечить актуальность требуемой конфигурации TeamsFx для добавленных ресурсов Azure.
* `.fx/projectSettings.json` обновляется для отслеживания доступных ресурсов в проекте.

После добавления ресурсов в проект появляются следующие дополнительные изменения:

|Ресурсы|Изменения|Описание|
|---------------|---------------|-----------------------------|
|Функции Azure|Код шаблона функций Azure будет добавлен во вложенную папку с путем `yourProjectFolder/api`</br></br>`launch.json` и `task.json` будут обновлены в папке `.visual studio code`.| Включает в проект шаблон триггера HTTP hello world.</br></br> Включает необходимые сценарии для Visual Studio Code, которые должны выполняться при отладке приложения в локальном режиме.|
|Управление API Azure|Файл спецификации открытого API добавлен во вложенную папку с путем `yourProjectFolder/openapi`|Определяет ваш API после публикации, это файл спецификации API.|

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов](provision.md)
* [Создание нового приложения Teams](create-new-project.md)
* [Добавление возможностей в приложения Teams](add-capability.md)
* [Развертывание в облаке](deploy.md)
