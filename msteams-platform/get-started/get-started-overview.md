---
title: Начало работы - Обзор
description: Обзор для начала работы Microsoft Teams документации разработчика
ms.localizationpriority: medium
ms.topic: reference
keywords: Microsoft Teams примерах разработчика
ms.openlocfilehash: ee986f04ca760fbf9090f7dda94e1378261db7df
ms.sourcegitcommit: e45742fd2aa2ff5e5c15e8f7c20cc14fbef6d441
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2021
ms.locfileid: "61075481"
---
# <a name="get-started"></a>Начало работы

Добро пожаловать на начало создания и развертывания настраиваемых приложений для Microsoft Teams!

Пройдитесь по шагам по созданию базового приложения Teams в реальном мире. The Get started also introduces you to common tools, fundamental concepts, and more advanced features.

Вот представление о том, что вы узнаете:

- Встать и быстро работать с Microsoft Teams набор средств (Visual Studio Code расширения).
- Получите опыт работы с набор средств и SDKs.
- Настройка и создание различных типов Teams приложений.

Давайте кратко рассмотрим параметры среды сборки, которые можно выбрать, и дорожную карту по созданию и развертыванию Teams приложения.

:::image type="content" source="../assets/images/get-started/gs-build-options.png" alt-text="На рисунке показаны основные действия по созданию и развертыванию Teams приложения.":::

## <a name="app-capabilities-and-development-tools"></a>Возможности и средства разработки приложений

В зависимости от возможностей приложения выберите соответствующий набор средств разработки.

| Возможности приложений | Взаимодействие пользователей | Рекомендуемые средства | Пакеты SDK | Стеки технологий / Языки |
|--------|-------------|--------|--------|--------|
| Вкладки | Полноэкранный встроенный веб-опыт. | VS Code с Teams набор средств или [CLI TeamsFx,](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) если вы предпочитаете использовать CLI | [TeamsFx SDK для](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) основных либов и Teams [клиента SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) для функций пользовательского интерфейса | Веб-технологии в целом, HTML, CSS и JavaScript (incl. React). |
| боты; | Чат-бот, который беседует с участниками. | VS Code с Teams набор средств или [CLI TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) и [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C#, Java и Python. |
| Расширения для система обмена сообщениями | Ярлыки для вставки внешнего контента в беседу или принятия действий по сообщениям. | VS Code с Teams набор средств или [CLI TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) и [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C#, Java и Python. |

*Вы не ограничены использованием этих определенных стеков!*

Если вы уже знакомы с рабочий процесс Yeoman, вы можете использовать [Генератор YoTeams Yeoman](https://github.com/pnp/generator-teams/blob/master/docs/docs/tutorials/build-your-first-microsoft-teams-app.md) для создания приложений.

> [!NOTE]
> Если вы используете App Studio, рекомендуем использовать портал разработчиков для настройки, распространения и управления Teams приложениями.


## <a name="build-your-first-teams-app"></a>Создайте первое Teams приложение

Теперь давайте создадим первое Teams приложение. Но сначала выберите язык (или рамки) и подготовьте среду разработки.

> [!div class="nextstepaction"]
> [Создайте приложение Teams javaScript с помощью React](../sbs-gs-javascript.yml)

> [!div class="nextstepaction"]
> [Создайте приложение Teams с помощью SPFx](../sbs-gs-spfx.yml)

> [!div class="nextstepaction"]
> [Создание приложения Teams с C# или .NET](../sbs-gs-csharp.yml)

> [!div class="nextstepaction"]
> [Создайте приложение Teams с помощью Node.js](../sbs-gs-nodejs.yml)
