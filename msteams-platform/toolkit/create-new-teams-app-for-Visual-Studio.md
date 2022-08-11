---
title: Создание приложения Teams в Visual Studio
author: surbhigupta
description: В этом модуле вы узнаете, как создать приложение Teams с помощью набора средств Teams для Visual Studio.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: 12f0b74726aed8cdca50d9f5c078acd0f22cbeaa
ms.sourcegitcommit: 52a11f7614c43172bc2d57401a60d569db5310a9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2022
ms.locfileid: "67291662"
---
# <a name="create-new-teams-app-in-visual-studio"></a>Создание приложения Teams в Visual Studio

Набор средств Teams предоставляет шаблоны приложений Microsoft Teams в Visual Studio для создания приложения Teams.  Вы можете выполнить поиск и выбрать шаблон приложения Teams, который требуется при создании нового проекта. У вас могут быть шаблоны приложений Teams для создания.

* Приложение tab
* Командный бот
* Бот уведомлений
* Расширение для сообщений

## <a name="prerequisites"></a>Предварительные требования

| &nbsp; | Установка | Для использования... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio версии 17.3 | Вы можете установить корпоративный выпуск Visual Studio и установить рабочую нагрузку ASP.NET и средства разработки Microsoft Teams. |
| &nbsp; | Набор средств Teams | Расширение Visual Studio, которое создает шаблон проекта для вашего приложения. Используйте последнюю версию. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams для взаимодействия в одном месте со всеми пользователями, с которыми вы работаете, с помощью приложений для чата, собраний и звонков. |
 | &nbsp; | [Подготовка клиента Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) | Доступ к учетной записи Teams с соответствующими разрешениями на установку приложения. |

1. Выберите **"Создать проект" в** разделе **"Начало работы** " при запуске Visual Studio.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project1.png" alt-text="Создание проекта с помощью функции &quot;Начало работы&quot;":::

   Вы также можете создать новый проект непосредственно из приложения.

1. Выберите **меню "Файл** ".
1. Выберите  **"Новое"**.
1. Выберите **"Проект"**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project2.png" alt-text="Создание проекта из меню &quot;Файл&quot;":::

1. Найдите приложение Microsoft **Teams** в списке.
1. Выберите **приложение Microsoft Teams**.
1. Нажмите кнопку **Далее**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app.png" alt-text="Поиск и выбор приложения Microsoft Teams":::

1. Выберите **имя проекта** и введите имя проекта.
1. Нажмите **Создать**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-project-name.png" alt-text="Имя приложения":::

1. Выберите тип **приложения Teams,** который вы хотите создать.
1. Нажмите **Создать**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-type.png" alt-text="Выбор типа приложения Teams":::

## <a name="teams-app-templates-in-teams-toolkit-for-visual-studio"></a>Шаблоны приложений Teams в Наборе средств Teams для Visual Studio

Вы можете увидеть шаблоны приложений Teams, уже заполненные в Наборе средств Teams для различных типов приложений Teams. В следующей таблице перечислены все доступные шаблоны:

|Шаблон приложения Teams  |Описание  |
|---------|---------|
|Бот уведомлений     |Приложение Бота уведомлений может отправлять уведомления клиенту Teams. Существует несколько способов активации уведомления. Например, можно активировать уведомление по HTTP-запросу или по времени. Вы также можете выбрать активируемую отправку уведомлений в зависимости от бизнес-сценария.         |
|Командный бот     |Пользователи могут ввести команду для взаимодействия с ботом с помощью приложения Command Bot.         |
|Tab     |Приложение tab отображает веб-страницу в Teams и включает единый вход с помощью учетной записи Teams.         |
|Расширение сообщения     |Приложение расширения сообщений реализует простые функции, такие как создание адаптивной карточки, поиск пакетов Изум, удаление ссылок для домена "dev.botframework.com".         |

> [!NOTE]
>После создания проекта набор средств Teams автоматически открывает командную строку "Начало работы". Теперь вы можете просмотреть инструкции в разделе "Начало работы" и просмотреть различные функции в Наборе средств Teams.

## <a name="see-also"></a>См. также

* [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
* [Развертывание приложения Teams в облаке с помощью Visual Studio](deploy-teams-app.md)
