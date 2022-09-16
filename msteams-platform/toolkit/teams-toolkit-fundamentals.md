---
title: Общие сведения о наборе средств Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете о наборе средств Teams, установке набора средств Teams и пути взаимодействия пользователя с Набором средств Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 95a42e4bd2064bc1ce4b775f13ba990890bc6776
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780732"
---
# <a name="teams-toolkit-overview"></a>Общие сведения о наборе средств Teams

Набор средств Teams — это функция возможностей, которая позволяет выполнять несколько функций как в Microsoft Visual Studio Code, так и в Visual Studio. С помощью Набора средств Teams можно автоматизировать процесс от создания до развертывания и настройки приложения. Различные функции и преимущества Набора средств Teams рассматриваются в соответствующей документации по нужным средам.

::: zone pivot="visual-studio-code"

## <a name="teams-toolkit-overview-for--visual-studio-code"></a>Обзор набора средств Teams для Visual Studio Code

Набор средств Teams позволяет создавать, отлаживать и развертывать приложение Teams прямо из Visual Studio Code. Разработка приложений с помощью набора средств имеет следующие преимущества:

* Интегрированное удостоверение
* Доступ к облачному хранилищу
* Данные из Microsoft Graph
* Службы Azure и Microsoft 365 с подходом без настройки.

Для разработки приложений Teams, аналогичной набору средств Teams для Visual Studio, вы можете использовать средство [CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), состоящее из `teamsfx` набора средств.

## <a name="user-journey-of-teams-toolkit"></a>Путь пользователя при применении набора средств Teams

Набор средств Teams автоматизирует ручную работу и обеспечивает отличную интеграцию ресурсов Teams и Azure. На следующем изображении показан путь пользователя при применении набора средств Teams.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Путь взаимодействия пользователя с набором средств Teams" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

Основные вехи этого пути:

1. Начало работы с создания проекта или применения примера приложения Teams.
1. Добавление возможностей или изменение файла манифеста при необходимости.
1. Использование учетной записи Microsoft 365 для создания и отладки приложения Teams.
1. Использование учетной записи Azure для подготовки и развертывания приложения в облаке.
1. Публикация приложения в Teams.

В следующей таблице приведены общие сведения о Наборе средств Teams в Visual Studio Code.

| Процесс | Описание |
| ---- | ---- |
| Установка Набора средств Teams | Набор средств Teams можно установить двумя способами: <br> — Использование Visual Studio Code <br> — Использование Visual Studio Code Marketplace|
| Поддержка сред сборки | У вас есть два разных типа среды: <br> — Javascript или Typescript <br> — SPFx |
| Поддержка типов приложений и функций Azure | Существует два разных типа приложений: <br> — Приложение на основе возможностей, например tab, bot, message extension  <br> — Приложение Teams на основе сценариев, например бот уведомлений, командный бот и личная вкладка с поддержкой единого входа |
| Разработка приложения Teams | Он содержит: <br> — Добавление среды и управление ими <br> — Создание приложения с несколькими возможностями <br> — создание облачных ресурсов на основе возможностей; <br> — интеграция стороннего API <br> — Настройка файла манифеста <br> — Пакет SDK для TeamsFx |
| Отладка приложения Teams | Он содержит: <br> — Локальная отладка приложения Teams <br> — Отладка фонового процесса|
| Размещение приложения Teams | Он содержит: <br> — подготовка ресурсов в облаке; <br> — Развертывание в облаке|
| Тестирование приложения Teams | Он содержит: <br> — Интеграция и свертывание <br> — Пакет метаданных Zip Teams <br> — Загрузка неопубликованного и тестового приложения в среде Teams <br> — Тестирование поведения приложения в разных средах|
| Публикация приложения Microsoft Teams | Он содержит: <br> — Публикация приложения <br> — Управление утверждением администратора <br> — Публикация в хранилище <br> — Интеграция с порталом разработчика |

### <a name="entities-integrated-with-teams-toolkit"></a>Сущности, интегрированные с Набором средств Teams

Набор средств Teams — это расширение в Visual Studio Code. Он интегрирован со следующими сущностями в Teams Toolkit.such as Azure AD и Microsoft 365, портал разработчика и Microsoft Graph. Все сущности интегрированы в Набор средств Teams и помогают пользователям создавать приложения.

| Объекты | Описание |
| ---- | ---- |
| Azure AD  | Azure Active Directory (Azure AD) — это облачная служба управления удостоверениями и доступом. Эта служба помогает сотрудникам получать доступ к внешним ресурсам, таким как Microsoft 365, портал Azure и тысячам других приложений SaaS. |
| Microsoft 365  | Учетная запись разработчика Teams при разработке приложения.|
| Портал разработчика | Портал разработчика для Teams является основным средством для настройки и распространения приложений Microsoft Teams и управления ими. На портале разработчика вы можете работать совместно с коллегами над приложением, настраивать среды выполнения и многое другое. |
| Microsoft Graph | Microsoft Graph открывает доступ к данным и средствам искусственного интеллекта в Microsoft 365. Благодаря этому вы получите единую модель программируемости, которую можно использовать для доступа к колоссальному объему данных в Microsoft 365, Windows и Enterprise Mobility + Security. |

Набор средств Teams объединяет в одном месте все инструменты, необходимые для создания приложения Teams.

## <a name="manage-your-apps-using-developer-portal"></a>Управление приложениями с помощью портала разработчика

Так как Набор средств Teams интегрирован с порталом разработчика, вы можете настраивать, распространять и управлять приложением с помощью портала разработчика для [Teams](../concepts/build-and-test/teams-developer-portal.md) в разделе DEPLOYMENT после создания приложения. Дополнительные сведения см. в [статье об управлении приложениями Teams с помощью портала разработчика](../concepts/build-and-test/manage-your-apps-in-developer-portal.md).

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="Портал разработчика":::

::: zone-end

::: zone pivot="visual-studio"

## <a name="teams-toolkit-overview-for-visual-studio"></a>Обзор набора средств Teams для Visual Studio

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

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png" alt-text="Путь взаимодействия пользователя с набором средств Teams" lightbox="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png":::

Основные вехи этого пути:

1. Вы можете начать с создания нового проекта или попробовать создать пример приложения Teams.
1. Затем при необходимости можно изменить код или файл манифеста.
1. Для создания и отладки приложения Teams можно использовать учетную запись Microsoft 365.
1. Для подготовки и развертывания приложения в облаке можно использовать учетную запись Azure.
1. Наконец, вы можете опубликовать приложение в Teams.

Следующие операции пока не поддерживаются в Наборе средств Teams для Visual Studio по сравнению с Набором средств Teams для Microsoft Visual Studio Code однако они запланированы в будущем.

* Добавьте другие возможности Teams в приложение Teams.
* Добавление дополнительных ресурсов Azure в приложение Teams
* Добавьте единый вход (SSO) в приложение Teams.
* Добавьте подключение API в приложение Teams.
* Настройте Microsoft Azure Active Directory (Azure AD) манифеста.
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

::: zone-end
