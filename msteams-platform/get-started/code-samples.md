---
title: Примеры кода приложения
description: Ссылки и описания примерных приложений для платформы Microsoft Teams разработчика
localization_priority: Normal
ms.topic: reference
keywords: Microsoft Teams примерах разработчика
ms.openlocfilehash: 09369123f23fc76b5e8c9fe3d5e89df56763d21f
ms.sourcegitcommit: 10380fc80d7f281d2892b3514f87d1bd05180496
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2021
ms.locfileid: "53373916"
---
# <a name="overview"></a>Обзор

В этом руководстве вы узнаете, как создать приложение с помощью React, Blazor, SPFx, C# или .NET, Node.js и Генератор Yeoman. Вы также научитесь создавать свой первый бот и расширение обмена сообщениями. В этом руководстве будут доступны несколько примеров кода для вкладок, ботов, расширений обмена сообщениями, веб-ок и соединители, а также Graph API, которые помогут настроить и настроить приложения. Кроме того, вы также можете обратиться к разделам Microsoft Learn, в которых можно расширить возможности платформы Teams, создав настраиваемые приложения.  

## <a name="getting-started-with-microsoft-learn"></a>Начало работы с Microsoft Learn

| **Возможности**| **Модуль Learn**|
|--------|-------------|
| Tabs — встроенные веб-опытом  |  [Создание встроенных веб-интерфейсов с вкладками для Microsoft Teams](/learn/modules/embedded-web-experiences/) |
| Веб-перехватчики и соединительные линии  |  [Подключение веб-служб к Microsoft Teams с помощью веб-перехватчиков и соединителей Office 365](/learn/modules/msteams-webhooks-connectors/) |
|Расширения для система обмена сообщениями  | [Целенаправленные взаимодействия в Microsoft Teams с использованием расширений для сообщений](/learn/modules/msteams-messaging-extensions/)  |
| Модули задач |  [Сбор входных данных Microsoft Teams с помощью модулей задач](/learn/modules/msteams-task-modules/) |
| Разговорные боты  | [Создание интерактивных ботов для бесед в Microsoft Teams](/learn/modules/msteams-conversation-bots/)  |

## <a name="build-your-first-microsoft-teams-app-overview"></a>Создание первого Microsoft Teams общего обзора приложения

На начало **занятий** вы узнаете, как создавать базовые Teams приложения. Каждый учебник включает в себя создание простого приложения Teams с общими средствами, фундаментальными концепциями и более продвинутыми функциями.

### <a name="teams-app-fundamentals"></a>Teams приложений

Платформа [Teams позволяет](../overview.md) создавать настраиваемые приложения. Некоторые распространенные сценарии для использования пользовательского приложения Microsoft Teams:

* внедрение веб-сайта или веб-приложения непосредственно в клиент Teams;
* Помогите пользователям быстро искать информацию в другой системе и добавлять результаты в беседу в Teams.
* запуск рабочих процессов на основе беседы в Teams с сохранением контекста беседы.

Прежде чем приступить к учебникам, вы должны знать следующее о создании приложений для Teams.

### <a name="app-capabilities"></a>Возможности приложений

Приложение Teams состоит из одной или более возможностей платформы и [точек](../concepts/capabilities-overview.md) [взаимодействия пользователей.](../concepts/extensibility-points.md)

В зависимости от возможностей приложения вам потребуется соответствующий инструментарий разработки.

| Возможности приложения | Взаимодействие пользователей | Рекомендуемые | SDKs | Технологические стеки | |--------|-------------|| --------|| --------|| --------| | Вкладки | Полноэкранный встроенный веб-опыт. | VS Code с Teams набор средств или YoTeams (Yeoman Generator) | [Teams клиента SDK |](/javascript/api/overview/msteams-client) Веб-технологии в целом, HTML, CSS и JavaScript | | Боты | Чат-бот, который беседует с участниками. | VS Code с Teams набор средств или YoTeams (Yeoman Generator) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C# или Python | | Расширения обмена сообщениями | Ярлыки для вставки внешнего контента в беседу или принятия действий по сообщениям. | VS Code с Teams набор средств или YoTeams (Yeoman Generator) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C# или Python |

В разделе Начало работы вы можете пройти через рекомендуемые наборы инструментов и часто используемые технологии, такие как Visual Studio Code с расширением Teams, React.js для вкладок и Node.js для ботов и расширений обмена сообщениями, хотя вы не ограничены использованием этих определенных стеков *.*

Если вы предпочитаете использовать интерфейс командной строки (CLI), см. в Microsoft Teams приложение с помощью генератора [Yeoman.](../get-started/get-started-yeoman.md)

### <a name="teams-does-not-host-your-app"></a>Teams не является хост-приложением

Вы установите только пакет приложений, содержащий файл конфигурации, называемый манифестом и значками приложений для Teams клиента. Остальные логики приложения и хранилища данных находятся в другом месте, например в Azure Web Services. Ваше приложение в облаке или локальном доступе во время доступа к Teams https.

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Иллюстрация, показывающая ваше Teams, показывает логику приложения на облачном сервере.":::

## <a name="see-also"></a>См. также

* [Создание приложения с React](first-app-react.md)
* [Создание приложения с помощью Blazor](first-app-blazor.md)
* [Создание приложения с SPFx](first-app-spfx.md)
* [Создание приложения с помощью C# или .NET](get-started-dotnet-app-studio.md)
* [Создайте приложение с помощью Node.js](get-started-nodejs-app-studio.md)
* [Создание приложения с помощью генератора Yeoman](get-started-yeoman.md)
* [Создание бота беседы](first-app-bot.md)
* [Создание расширения для обмена сообщениями](first-message-extension.md)
* [Примеры кода](https://github.com/OfficeDev/Microsoft-Teams-Samples)