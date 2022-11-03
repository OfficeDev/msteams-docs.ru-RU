---
title: Общие сведения о наборе средств Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете о наборе средств Teams, установке набора средств Teams и пользовательском пути набора средств Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: cb3508bdd22f9d05c48e71b1b90ec4ffbf4c56af
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833165"
---
# <a name="teams-toolkit-overview"></a>Общие сведения о наборе средств Teams

Набор средств Teams упрощает начало разработки приложений для Microsoft Teams с помощью Visual Studio и Visual Studio Code.

* Начните с шаблона проекта или из примера.
* Экономия времени настройки с помощью автоматической регистрации и настройки приложений.
* Запуск и отладка в Teams непосредственно из знакомых средств.
* Интеллектуальные значения по умолчанию для размещения в Azure с использованием инфраструктуры как кода и Bicep.
* Создавайте уникальные конфигурации, такие как разработка, тестирование и разработка, с помощью функции "Среды".
* Перенос приложения в организацию или в App Store Teams с помощью встроенных средств публикации.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Путь взаимодействия пользователя с набором средств Teams" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

## <a name="available-for-visual-studio-and-visual-studio-code"></a>Доступно для Visual Studio и Visual Studio Code

Набор средств Teams доступен бесплатно для Visual Studio Code и поддерживает Visual Studio 2022 Community, Professional и Enterprise. Дополнительные сведения об установке и настройке см. в [документации по установке набора средств Teams](./install-Teams-Toolkit.md) .

| Набор средств Teams | Visual Studio | Visual Studio Code |
| - | ------------- | ------------------ |
| Установка | Доступно в Visual Studio Installer | Доступно в VS Marketplace |
| Сборка с помощью | C#, .NET, ASP.NET, Blazor | JavaScript, TypeScript, React, SPFx |

## <a name="features"></a>Возможности

### <a name="project-templates"></a>Шаблоны проектов

Набор средств Teams упрощает работу с шаблонами для распространенных бизнес-сценариев приложений и интеллектуальных значений по умолчанию, чтобы ускорить работу. Если вы уже знакомы с разработкой приложений Teams, вы также можете начать непосредственно с шаблонов, ориентированных на возможности. т. е. tab, bot, расширение для обмена сообщениями.

::: zone pivot="visual-studio-code"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app.png" alt-text="Меню &quot;Создание приложения Teams&quot; в VS Code":::
::: zone-end

::: zone pivot="visual-studio"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app-vs.png" alt-text="Меню &quot;Создание приложения Teams&quot; в VS Code":::
::: zone-end

### <a name="automatic-registration-and-configuration"></a>Автоматическая регистрация и настройка

Сэкономить время и позволить набору средств автоматически зарегистрировать приложение на портале разработчика Teams и настроить параметры, например Azure Active Directory, автоматически при первом запуске или отладке приложения. Войдите с помощью учетной записи Microsoft 365, чтобы контролировать, где настроено приложение, и настраивать включенный манифест Azure AD, когда требуется дополнительная гибкость.

::: zone pivot="visual-studio-code"

### <a name="multiple-environments"></a>Несколько сред

С помощью функций Среды можно создавать различные группы облачных ресурсов, чтобы упростить запуск и тестирование приложения. Используйте среду разработки с подпиской Azure или создайте новую с другой подпиской для промежуточной, тестовой и рабочей.

### <a name="quick-access-to-teams-developer-portal"></a>Быстрый доступ к порталу разработчика Teams

Быстрый доступ к порталу разработчика Teams, где можно настраивать, распространять приложения и управлять ими. Дополнительные сведения см. в статье [Управление приложениями Teams с помощью портала разработчика](../concepts/build-and-test/manage-your-apps-in-developer-portal.md).

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="Портал разработчика":::

::: zone-end

::: zone pivot="visual-studio"

#### <a name="teamsfx-net-sdk-reference-docs"></a>Справочная документация по пакету SDK для TeamsFx для .NET

* [Пространство имен Microsoft.Extensions.DependencyInjection](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Пространство имен Microsoft.TeamsFx](/../dotnet/api/Microsoft.TeamsFx)
* [Пространство имен Microsoft.TeamsFx.Configuration](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Пространство имен Microsoft.TeamsFx.Conversation](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Пространство имен Microsoft.TeamsFx.Helper](/../dotnet/api/Microsoft.TeamsFx.Helper)

::: zone-end

## <a name="see-also"></a>См. также

* [Создание приложения Teams в Visual Studio](create-new-project.md)
* [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
* [Развертывание приложения Teams в облаке с помощью Visual Studio](deploy.md)
