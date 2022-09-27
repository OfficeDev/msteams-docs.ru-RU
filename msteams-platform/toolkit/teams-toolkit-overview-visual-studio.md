---
title: Обзор набора средств Teams для Visual Studio
author: surbhigupta
description: В этом модуле вы ознакомитесь с обзором набора средств Teams для Visual Studio
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
ms.openlocfilehash: 3685d105f13024507b880c35040b9d798a6d845f
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027449"
---
# <a name="teams-toolkit-overview-for-visual-studio"></a>Обзор набора средств Teams для Visual Studio

Набор средств Teams для Visual Studio помогает создавать, отлаживать и развертывать приложения Microsoft Teams. Набор средств Teams для Visual Studio является общедоступным в Visual Studio 2022 версии 17.3. Разработка приложений с помощью Набора средств Teams имеет следующие преимущества:

* Интегрированное удостоверение
* Доступ к облачному хранилищу
* Данные из Microsoft Graph
* Службы Azure и Microsoft 365 с использованием подхода с нулевой конфигурацией

Для разработки приложений Teams можно также использовать средство [интерфейса командной](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) строки, аналогичное набору средств Teams для Microsoft Visual Studio Code, включающее toolkit `teamsfx`.

Набор средств Teams объединяет все средства, необходимые для создания приложения Teams.

> [!NOTE]
> Набор средств Teams недоступен в других версиях.

## <a name="user-journey-of-teams-toolkit"></a>Путь взаимодействия пользователя с набором средств Teams

Набор средств Teams автоматизирует ручную работу и обеспечивает отличная интеграция Ресурсов Teams и Azure. На следующем рисунке показан путь взаимодействия пользователя:

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png" alt-text="Путь взаимодействия пользователя с набором средств Teams":::

Основные вехи этого пути:

1. Вы можете начать с создания нового проекта или попробовать создать пример приложения Teams.
1. Затем при необходимости можно изменить код или файл манифеста.
1. Для создания и отладки приложения Teams можно использовать учетную запись Microsoft 365.
1. Для подготовки и развертывания приложения в облаке можно использовать учетную запись Azure.
1. Наконец, вы можете опубликовать приложение в Teams.

## <a name="install-teams-toolkit-for-visual-studio"></a>Установка набора средств Teams для Visual Studio

Последнюю версию установщика Visual Studio можно скачать со страницы [скачивания Visual Studio](https://visualstudio.microsoft.com).

> [!NOTE]
> Перед установкой Visual Studio необходимо сначала установить установщик Visual Studio.

После открытия установщика Visual Studio во всплывающем окне "Рабочие нагрузки".

1. Установите флажок **ASP.NET и рабочей нагрузки веб-разработки** .
1. Выберите поле " **Средства разработки Microsoft Teams** " на панели сведений об установке.
1. Нажмите кнопку **Установить**.

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install1.png" alt-text="Установка Visual Studio":::

1. Нажмите **кнопку "** Запустить", чтобы открыть Visual Studio.

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch.png" alt-text="Запуск Visual Studio":::

   > [!IMPORTANT]
   > Рекомендуется скачать Visual Studio 2022 версии 17.3.0, так как Набор средств Teams для Visual Studio является общедоступным в этой версии. Эта статья написана для Visual Studio 2022 версии 17.3.0. Набор средств Teams версии 17.3.* или более поздней.

## <a name="take-a-tour-of-teams-toolkit"></a>Обзор набора средств Teams

После установки Набора средств Teams можно просмотреть различные параметры меню Набора средств Teams:

1. Выберите **"Проект"**.
1. Выберите **Набор средств Teams**.
1. Теперь вы можете получить доступ к **пунктам меню "Набор средств Teams** ".

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu.png" alt-text="Меню операций набора средств Teams":::

   Вы также можете получить доступ к меню Teams Toolkit из Обозреватель решений.

4. Щелкните правой кнопкой **мыши проект**.
5. Выберите **пункты меню** >  "Набор средств **Teams**".

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu1.png" alt-text="Операции с набором средств Teams из Project":::

   > [!NOTE]
   > В этом сценарии имя проекта **— MyTeamsApp1**.

В Наборе средств Teams для Visual Studio можно выполнять следующие функции:

|Функция  |Описание  |
|---------|---------|
|Создание проекта Teams     |Создание проекта Teams с помощью шаблона Teams в Visual Studio         |
|Подготовка зависимостей приложений Teams     |Перед выполнением локальной отладки этот шаг помогает настроить зависимости локальной отладки и зарегистрировать приложение Teams на платформе Teams. Вам нужна учетная запись Microsoft 365. Дополнительные сведения см. в статье ["Отладка приложения Teams в локальной среде с помощью Visual Studio"](debug-teams-app-visual-studio.md).         |
|Открытие файла манифеста     |Чтобы открыть файл манифеста Teams, можно навести указатель мыши на параметры, чтобы просмотреть значения. Дополнительные сведения см. в статье ["Изменение манифеста приложения Teams с помощью Visual Studio"](VS-TeamsFx-preview-and-customize-app-manifest.md).         |
|Обновление манифеста на портале разработчика Teams     |При обновлении файла манифеста только после этого можно повторно развернуть файл манифеста в Azure без повторного развертывания всего проекта. Используйте эту команду, чтобы обновить изменения на удаленном компьютере. Дополнительные сведения см. в статье ["Изменение манифеста приложения Teams с помощью Visual Studio"](VS-TeamsFx-preview-and-customize-app-manifest.md).       |
|Подготовка к работе в облаке     |Этот параметр поможет вам создать ресурсы Azure, на которых размещено приложение Teams. Дополнительные сведения см. в [разделе "Подготовка облачных ресурсов с помощью Visual Studio"](provision-cloud-resources.md).        |
|Развертывание в облаке     |Этот параметр позволяет скопировать код в ресурсы Azure, созданные при выполнении действия "Подготовка в облаке". Дополнительные сведения см[. в статье "Развертывание приложения Teams в облаке с помощью Visual Studio"](deploy-teams-app.md).        |
|Предварительная версия в Teams     |Этот параметр запускает веб-клиент Teams и позволяет просматривать приложение Teams в браузере.         |
|Zip-пакет приложения     |Этот параметр создает пакет приложения Teams в папке `Build` в проекте. Вы можете отправить пакет в клиент Teams и запустить приложение Teams.         |

Приведенные ниже операции пока не поддерживаются в Наборе средств Teams для Visual Studio по сравнению с набором средств Teams для Visual Studio Code, однако они запланированы в будущем.

* Добавьте другие возможности Teams в приложение Teams.
* Добавление дополнительных ресурсов Azure в приложение Teams
* Добавьте единый вход в приложение Teams.
* Добавьте подключение API в приложение Teams.
* Настройка Azure AD манифеста.
* Добавьте конвейеры CI/CD.
* Управление несколькими облачными средами.
* Совместная работа над проектами Teams.
* Публикация приложения Teams.

### <a name="teamsfx-net-sdk-reference-docs"></a>Справочные материалы по пакету SDK для TeamsFx для .NET

* [Пространство имен Microsoft.Extensions.DependencyInjection](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Пространство имен Microsoft.TeamsFx](/../dotnet/api/Microsoft.TeamsFx)
* [Пространство имен Microsoft.TeamsFx.Configuration](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Пространство имен Microsoft.TeamsFx.Conversation](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Пространство имен Microsoft.TeamsFx.Helper](/../dotnet/api/Microsoft.TeamsFx.Helper)

## <a name="see-also"></a>См. также

* [Создание приложения Teams в Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
* [Развертывание приложения Teams в облаке с помощью Visual Studio](deploy-teams-app.md)
