---
title: Общие сведения о наборе средств Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете о наборе средств Teams, установке набора средств Teams и пути взаимодействия пользователя с Набором средств Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 84a18c736c59c992bb4e3e51962ed631483f7f2b
ms.sourcegitcommit: 3aaccc48906fc6f6fbf79916af5664bf55537250
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/30/2022
ms.locfileid: "68296027"
---
# <a name="teams-toolkit-overview"></a>Общие сведения о наборе средств Teams

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Путь взаимодействия пользователя с набором средств Teams" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

Набор средств Teams упрощает начало разработки приложений для Microsoft Teams с помощью Visual Studio и Visual Studio Code.

* Начните с шаблона проекта или из примера
* Экономия времени установки с помощью автоматической регистрации и настройки приложения
* Запуск и отладка в Teams непосредственно из знакомых средств
* Интеллектуальные значения по умолчанию для размещения в Azure с использованием инфраструктуры как кода и Bicep
* Создание уникальных конфигураций, таких как разработка, тестирование и prod, с помощью функции "Среды"
* Перенос приложения в организацию или App Store Teams с помощью встроенных средств публикации

## <a name="available-for-visual-studio-and-visual-studio-code"></a>Доступно для Visual Studio и Visual Studio Code

Набор средств Teams доступен бесплатно для Visual Studio Code и поддерживает Visual Studio 2022 Community, Professional и Enterprise. Дополнительные сведения [об установке](./install-Teams-Toolkit.md) и настройке см. в документации по установке Набора средств Teams.

| Набор средств Teams | Visual Studio | Visual Studio Code |
| - | ------------- | ------------------ |
| Установка | Доступно в Visual Studio Installer | Доступно в VS Marketplace |
| Выполните сборку с помощью | C#, .NET, ASP.NET, Blazor | JavaScript, TypeScript, React, SPFx |

## <a name="features"></a>Возможности

### <a name="project-templates"></a>Шаблоны проектов

Набор средств Teams упрощает начало работы с шаблонами для распространенных бизнес-сценариев приложений и интеллектуальными значениями по умолчанию, чтобы ускорить переход на рабочую среду. Если вы уже знакомы с разработкой приложений Teams, вы также можете начать непосредственно с шаблонов, ориентированных на возможности. Например, Tab, Bot, Messaging Extension.

::: zone pivot="visual-studio-code"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app.png" alt-text="Создание меню приложения Teams в VS Code":::
::: zone-end

::: zone pivot="visual-studio"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app-vs.png" alt-text="Создание меню приложения Teams в VS Code":::
::: zone-end

### <a name="automatic-registration-and-configuration"></a>Автоматическая регистрация и настройка

Экономите время и позвольте набору средств автоматически зарегистрировать приложение на портале разработчика Teams и автоматически настроить такие параметры, как Azure Active Directory при первом запуске или отладке приложения. Войдите с помощью учетной записи Microsoft 365, чтобы контролировать, где настроено приложение, и настраивать включенный Azure AD, когда требуется больше гибкости.

::: zone pivot="visual-studio-code"

### <a name="multiple-environments"></a>Несколько сред

С помощью функций "Среды" можно создавать различные группы облачных ресурсов, упрощая запуск и тестирование приложения. Используйте среду разработки с подпиской Azure или создайте новую с другой подпиской для промежуточной, тестовой и рабочей среды.

### <a name="quick-access-to-teams-developer-portal"></a>Быстрый доступ к порталу разработчика Teams

Быстрый доступ к порталу разработчика Teams, где можно настраивать, распространять и управлять приложением. Дополнительные сведения см. в [статье об управлении приложениями Teams с помощью портала разработчика](../concepts/build-and-test/manage-your-apps-in-developer-portal.md).

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="Портал разработчика":::

::: zone-end

::: zone pivot="visual-studio"

#### <a name="teamsfx-net-sdk-reference-docs"></a>Справочные материалы по пакету SDK для TeamsFx для .NET

* [Пространство имен Microsoft.Extensions.DependencyInjection](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Пространство имен Microsoft.TeamsFx](/../dotnet/api/Microsoft.TeamsFx)
* [Пространство имен Microsoft.TeamsFx.Configuration](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Пространство имен Microsoft.TeamsFx.Conversation](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Пространство имен Microsoft.TeamsFx.Helper](/../dotnet/api/Microsoft.TeamsFx.Helper)

::: zone-end

## <a name="see-also"></a>См. также

* [Создание приложения Teams в Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
* [Развертывание приложения Teams в облаке с помощью Visual Studio](deploy-teams-app.md)
