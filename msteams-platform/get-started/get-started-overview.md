---
title: Начало работы — обзор
description: Обзор начала работы с документацией разработчика Microsoft Teams
ms.localizationpriority: high
ms.topic: reference
keywords: Примеры для разработчиков Microsoft Teams
ms.openlocfilehash: 9e4405439241de9a4f3db97d256df8b8fab21880
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757712"
---
# <a name="get-started"></a>Начало работы

Добро пожаловать в раздел "Начало работы" для создания и развертывания пользовательских приложений для Microsoft Teams!

Выполните шаги по созданию базового приложения Teams в реальных условиях. Раздел "Начало работы" также знакомит вас с общими инструментами, базовыми концепциями и расширенными возможностями.

Вот о чем пойдет речь в этом разделе:

- быстрое налаживание работы с набором средств Microsoft Teams (расширение Visual Studio Code);
- навыки использования набора средств и пакетов SDK;
- настройка и сборка различных типов приложений Teams.

Давайте кратко рассмотрим варианты среды сборки, которые вы можете выбрать, и дорожную карту для создания и развертывания приложения Teams.

:::image type="content" source="../assets/images/get-started/gs-build-options.png" alt-text="Иллюстрация: основные шаги по созданию и развертыванию приложения Teams":::

## <a name="app-capabilities-and-development-tools"></a>Возможности и средства разработки приложений

В зависимости от возможностей, которые должно иметь приложение, выберите соответствующий набор средств разработки.

| Возможности приложений | Действия пользователя | Рекомендуемые средства | Пакеты SDK | Стеки технологий/Языки |
|--------|-------------|--------|--------|--------|
| Вкладки | Полноэкранный встроенный веб-интерфейс. | Microsoft Visual Studio Code с расширением набора средств Teams или [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), если вы предпочитаете использовать CLI | [Пакет SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) для основных библиотек и [пакет SDK клиента Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) для функций пользовательского интерфейса | Веб-технологии в целом, HTML, CSS и JavaScript (включая React). |
| Боты | Чат-бот, который беседует с участниками. | Visual Studio Code с расширением набора средств Teams или [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [Пакет SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) и [пакет SDK Bot Framework](https://dev.botframework.com/) | Node.js, C#, Java и Python. |
| Расширения для сообщений | Ярлыки для вставки внешнего контента в беседу или выполнения действий с сообщениями. | Visual Studio Code с расширением набора средств Teams или [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [Пакет SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) и [пакет SDK Bot Framework](https://dev.botframework.com/) | Node.js, C#, Java и Python. |

*Вы не ограничены использованием этих конкретных стеков!*

Если вы уже знакомы с рабочим процессом Yeoman, возможно, вы предпочтете использовать [генератор Yeoman YoTeams](https://github.com/pnp/generator-teams/blob/master/docs/docs/tutorials/build-your-first-microsoft-teams-app.md) для создания приложений.

> [!WARNING]
> Если вы использовали App Studio, рекомендуем попробовать Портал разработчика для настройки, распространения и управления приложениями Teams.<br> App Studio станет не рекомендованной к использованию не позднее 30 июня 2022 г.

## <a name="build-your-first-teams-app"></a>Создайте свое первое приложение Teams

Теперь давайте создадим ваше первое приложение Teams. Но сначала выберите язык (или платформу) и подготовьте среду разработки.

> [!div class="nextstepaction"]
> [Создайте приложение с вкладками Teams с JavaScript, используя React](../sbs-gs-javascript.yml)
> [!div class="nextstepaction"]
> [Создайте бот-приложение Teams с JavaScript, используя React](../sbs-gs-bot.yml)
> [!div class="nextstepaction"]
> [Создайте приложение расширения сообщений Teams с JavaScript, используя React](../sbs-gs-msgext.yml)
> [!div class="nextstepaction"]
> [Создание приложения Teams с помощью Blazor](../sbs-gs-blazorupdate.yml)
> [!div class="nextstepaction"]
> [Создание приложения Teams с помощью SPFx](../sbs-gs-spfx.yml)
> [!div class="nextstepaction"]
> [Создание приложения Teams с помощью C# или .NET](../sbs-gs-csharp.yml)
> [!div class="nextstepaction"]
> [Создание приложения Teams с помощью Node.js](../sbs-gs-nodejs.yml)
> [!div class="nextstepaction"]
> [Создание бота уведомлений с помощью JavaScript](../sbs-gs-notificationbot.yml)
> [!div class="nextstepaction"]
> [Создание командного бота с помощью JavaScript](../sbs-gs-commandbot.yml)
> [!div class="nextstepaction"]

## <a name="see-also"></a>См. также

* [Примеры Microsoft Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples#microsoft-teams-samples)
* [Ресурсы Git и GitHub](/contribute/additional-resources)
