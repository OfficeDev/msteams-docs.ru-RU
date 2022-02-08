---
title: Создание приложений с помощью Teams набор средств и Visual Studio
description: Начало создания больших пользовательских приложений непосредственно Visual Studio с Microsoft Teams набор средств. Научитесь настраивать приложение в Visual Studio, проверять приложение и публиковать его с Visual Studio и портала разработчиков.
keywords: набор инструментов для визуальной студии teams
ms.localizationpriority: medium
ms.topic: overview
ms.author: johmil
ms.openlocfilehash: 2fa11fbf0b4bfb3d7c9b4fe376b6517e0313338f
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435854"
---
# <a name="build-apps-with-the-teams-toolkit-and-microsoft-visual-studio"></a>Создание приложений с помощью Teams набор средств и Microsoft Visual Studio

Набор средств Microsoft Teams Toolkit позволяет создавать пользовательские приложения Teams непосредственно в интегрированной среде разработки (IDE) Visual Studio. Этот набор средств Microsoft Teams предоставит вам пошаговые инструкции в процессе создания приложения, а также все необходимое для сборки, отладки и запуска вашего приложения Teams.

## <a name="prerequisites"></a>Предварительные требования

1. [Включить предварительный просмотр разработчика](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).

2. Убедитесь, что **<span>ASP.NET</span>** и модуль веб-разработки был добавлен в экземпляр Visual Studio. Дополнительные сведения см. в [Visual Studio изменения, добавляя](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) или удаляя рабочие нагрузки и компоненты.

![Модуль visual studio asp.net](../assets/images/visual-studio-web-dev-module.png)

## <a name="install-the-teams-toolkit"></a>Установка Teams набор средств

Приложение Microsoft Teams набор средств для Visual Studio доступно для скачивания с [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit) или непосредственно из меню Расширения в Visual Studio.

## <a name="use-the-toolkit"></a>Использование набора средств

- [Настройка нового проекта](#set-up-a-new-teams-project)
- [Настройка приложения](#configure-your-app)
- [Запустите приложение в Teams](#install-and-run-your-app-locally)
- [Проверка приложения](#validate-your-app)
- [Публикация приложения](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Настройка нового проекта Teams

1. Запуск Visual Studio 2019 г.
2. Выберите **Создание нового проекта**.
3. Поиск Microsoft Teams **app и** выберите **Далее**.
4. В **настройках нового проекта** введите имя **Project,** **Location** и **Solution**.
5. Выберите **Далее** , чтобы ввести имя приложения.
6. На экране Дополнительные сведения введите **имя приложения** и имя  разработчика или компании для Teams приложения.

## <a name="configure-your-app"></a>Настройка приложения

В основе приложения Teams три компонента:

- Клиент Microsoft Teams (веб-, настольный или мобильный), где пользователи взаимодействуют с вашим приложением.
- Сервер, который отвечает на запросы о контенте, отображаемом в Teams. Например, содержимое htmL-вкладок или адаптивная карта бота.
- Пакет Teams состоит из трех файлов:

    > [!div class="checklist"]
    >
    > - Manifest.json
    > - [Значок цвета](../resources/schema/manifest-schema.md#icons) для отображения приложения в каталоге общедоступных или организаций.
    > - [Значок плана](../resources/schema/manifest-schema.md#icons) для отображения на панели Teams действий.

При установке приложения клиент Teams определяет файл манифеста, чтобы определить необходимые сведения, такие как имя приложения и URL-адрес, в котором находятся службы.

> [!NOTE]
>Если вы еще этого не сделали, необходимо войти в Microsoft 365 учетную запись, чтобы продолжить процесс разработки.
>
> Если у вас нет Microsoft 365 учетной записи, вы можете подписаться на подписку [Microsoft 365 разработчика](https://developer.microsoft.com/microsoft-365/dev-program). Он бесплатный в течение 90 дней и обновляется до тех пор, пока вы используете его для разработки. Если у вас есть подписка Visual Studio Enterprise или Professional, обе программы включают бесплатную подписку Microsoft 365 разработчика[,](https://aka.ms/MyVisualStudioBenefits) активную для Visual Studio подписки. Дополнительные сведения см. [в Microsoft 365 подписки разработчика](/office/developer-program/office-365-developer-program-get-started).

### <a name="configuration-steps"></a>Этапы конфигурации

1. Чтобы настроить приложение, выберите Project > **TeamsFx > для меню SSO...**

При запросе впишитесь в свою учетную запись Майкрософт с клиентом M365.

## <a name="install-and-run-your-app-locally"></a>Установка и локальное запуск приложения

Нажмите кнопку F5, чтобы начать отладку. Диалоговое окно установки приложения отображается в Teams клиенте.

## <a name="validate-your-app"></a>Проверка приложения

Меню **Project > TeamsFx Validate > Teams Манифест** позволяет проверить, действителен ли пакет приложений.

## <a name="publish-your-app-to-teams"></a>Опубликуйте свое приложение в Teams

На [портале Teams](https://dev.teams.microsoft.com/home) разработчиков вы можете загрузить приложение в команду, отправить приложение в свой магазин пользовательских приложений для пользователей в организации или отправить приложение в App Source для всех Teams пользователей.

- ИТ-администратор проверит эти отправленные приложения.
- Вы можете вернуться на страницу **Публикация** , чтобы проверить состояние отправки и узнать, было ли ваше приложение утверждено или отклонено вашим ИТ-администратором. Здесь также можно отправлять обновления в приложение или отменять активные в настоящее время отправки.
