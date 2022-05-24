---
title: Добавление ресурсов в Teams приложения
author: MuyangAmigo
description: Описывает добавление ресурсов для набор средств Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: f3b96b60447596eae8c1cdf37f4b38f6653c444b
ms.sourcegitcommit: 74623035d7c18194e339f566c820e0653bc3d8b6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656651"
---
# <a name="add-cloud-resources-to-teams-app"></a>Добавление облачных ресурсов в приложение Teams

TeamsFx помогает подготовить облачные ресурсы для размещения приложения. При необходимости можно добавить облачные ресурсы, которые соответствуют вашим потребностям разработки.

## <a name="advantages"></a>Преимущества

Следующий список дает преимущества для добавления дополнительных облачных ресурсов в TeamsFx:

* Обеспечивает удобство
* Автоматически создает все файлы конфигурации и подключается к Teams с помощью Teams Toolkit

## <a name="limitation"></a>Ограничение

Если вы создали SPFx вкладку, вы не сможете добавить облачные ресурсы Azure.

## <a name="add-cloud-resources"></a>Добавление облачных ресурсов

**Добавить облачные ресурсы можно следующими способами:**

* Добавление облачных ресурсов с помощью Teams Toolkit в Visual Studio Code
* Добавление облачных ресурсов с помощью палитры команд

  > [!NOTE]
  > После успешного добавления ресурса в приложение Teams подготовку для каждой среды.
  
* **Чтобы добавить облачные ресурсы с помощью Teams Toolkit в Visual Studio Code:**

   1. Откройте **Visual Studio Code**.
   1. Выберите **Teams toolkit на** левой панели.
   1. Выберите **"Добавить компоненты"** в разделе **"РАЗРАБОТКА"**.

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/select-feature-updated.png" alt-text="добавление функции" border="true":::

* **Чтобы добавить облачные ресурсы с помощью палитры команд, выполните следующие действия.**

   1. Откройте **палитру команд**.
   1. **Введите Teams:Add.**
   1. Нажмите клавишу **ВВОД**.

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/Teams-add-features.png" alt-text="Облако" border="true":::

   1. Во всплывающем окне выберите облачные ресурсы для добавления в проект.

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/updated-final-cloud.png" alt-text="Окончательный" border="true":::

## <a name="add-cloud-resources-using-teamsfx-cli"></a>Добавление облачных ресурсов с помощью Командной строки TeamsFx

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

- [Функции Azure](/azure/azure-functions/functions-overview): бессерверное решение для удовлетворения требований по запросу, таких как создание веб-API для серверной части приложений Teams.
- [База данных SQL Azure](/azure/azure-sql/database/sql-database-paas-overview): ядро СУБД "платформа как услуга" (PaaS), которое служит хранилищем данных приложений Teams.
- [Управление API Azure](deploy.md). Шлюз API можно использовать для администрирования API, созданных для Teams приложений, и их публикации для использования в других приложениях, таких как приложения Power.
- [Azure Key Vault](/azure/key-vault/general/overview): защита криптографических ключей и других паролей, используемых облачными приложениями и службами.

## <a name="add-cloud-resources"></a>Добавление облачных ресурсов

После добавления ресурсов в проект появляются следующие изменения:

- Новые параметры, добавленные в azure.parameter. {env}.json для предоставления необходимых сведений для подготовки.
- Новое содержимое включается в шаблон ARM `templates/azure`, за исключением того, `templates/azure/teamsfx` что файлы находятся в папке для добавления ресурсов Azure.
- Файлы в папке `templates/azure/teamsfx` будут созданы повторно, чтобы обеспечить актуальность требуемой конфигурации TeamsFx для добавленных ресурсов Azure.
- `.fx/projectSettings.json` обновляется для отслеживания доступных ресурсов в проекте.

После добавления ресурсов в проект появляются следующие дополнительные изменения:

|Ресурсы|Изменения|Описание|
|---------------|---------------|-----------------------------|
|Функции Azure|Код шаблона функций Azure будет добавлен во вложенную папку с путем `yourProjectFolder/api`</br></br>`launch.json` и `task.json` будут обновлены в папке `.visual studio code`.| Включает в проект шаблон триггера HTTP hello world.</br></br> Включает необходимые сценарии для Visual Studio Code, которые должны выполняться при отладке приложения в локальном режиме.|
|Управление API Azure|Файл спецификации открытого API добавлен во вложенную папку с путем `yourProjectFolder/openapi`|Определяет ваш API после публикации, это файл спецификации API.|

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов](provision.md)
* [Создание нового приложения Teams](create-new-project.md)
* [Добавление возможностей для Teams приложений](add-capability.md)
* [Развертывание в облаке](deploy.md)