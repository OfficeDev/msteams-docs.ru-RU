---
title: Начало работы - Необходимые условия
author: adrianhall
description: Узнайте, как начать работу с разработкой Microsoft Teams и настроить среду.
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 73d99f2bbbc69bf13242110a56e13e662655283c
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646773"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a>Необходимые условия: начало разработки Microsoft Teams приложения

Перед созданием первого Teams необходимо установить несколько инструментов и настроить среду разработки.

## <a name="install-required-tools"></a>Установка необходимых средств

Некоторые из необходимых инструментов зависят от того, как вы предпочитаете создавать Teams приложение:

- [Node.js](https://nodejs.org/en/download/) (используйте последний выпуск V14 LTS) 
- Браузер с средствами разработчика , такими как [Microsoft Edge](https://www.microsoft.com/edge) (рекомендуется) или [Google Chrome](https://www.google.com/chrome/)
- Если вы разрабатываете с Помощью JavaScript, TypeScript или SharePoint Framework (SPFx), установите Visual Studio Code [версии](https://code.visualstudio.com/download)1.55 или более поздней версии.  
- Если вы разрабатываете с помощью .NET, установите Visual Studio [2019](https://visualstudio.com/download).  Убедитесь, что ASP.NET **и веб-разработки** или **межплатформеной** рабочей нагрузки .NET Core.

> [!WARNING]
> Известны проблемы с пакетом `npm@7` с node v15 и более поздним пакетом. Если у вас возникли проблемы с запуском, убедитесь, что `npm install` вы используете узел v14 (LTS)

## <a name="install-the-teams-toolkit"></a>Установка Teams набор средств

Этот Teams набор средств упрощает процесс разработки с помощью средств для обеспечения и развертывания облачных ресурсов для приложения, публикации в Teams магазине и других. Инструментарий можно использовать с помощью Visual Studio Code, Visual Studio или CLI `teamsfx` (называется).

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Откройте Visual Studio Code.
1. Выберите представление Расширения **(Ctrl+Shift+X**  /  **⌘⇧-X** или **> расширения).**
1. В поле поиска введите _Teams набор средств_.
1. Выберите на зеленой кнопке установки рядом с Teams набор средств.

Вы также можете найти Teams набор средств на Visual Studio Code [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

Следующие средства будут установлены расширением Visual Studio Code при необходимости.  Если уже установлено, вместо нее будет использоваться установленная версия.  Если используется Linux (в том числе WSL), необходимо установить эти средства перед использованием:

- [Основные средства Azure Functions](/azure/azure-functions/functions-run-local)

    Основные средства Azure Functions используются для локального запуска отлаженных компонентов, включая помощников проверки подлинности, необходимых при запуске служб в Azure.  Он устанавливается в каталоге проекта (с помощью `devDependencies` npm).

- [SDK .NET](/dotnet/core/install/)

    SDK .NET используется для установки настраиваемых привязки для локального отладки и развертывания приложений Azure Functions.  Если вы не установили SDK .NET 3.1 (или более поздней версии) глобально, портативная версия будет установлена.

- [ngrok](https://ngrok.com/download)

    Некоторые Teams приложения (беседные боты, расширения обмена сообщениями и входящие веб-оки) требуют входящих подключений.  Необходимо подвергать систему разработки Teams через туннель.  Туннель не требуется для приложений, которые включают только вкладки.  Этот пакет устанавливается в каталоге проекта (с помощью `devDependencies` npm).

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Вы можете использовать Visual Studio 2019 для разработки Teams с помощью Blazor Server в .NET.  Если вы не собираетесь разрабатывать Teams приложения в .NET, установите Visual Studio Code версию Teams набор средств.

Чтобы установить расширение Teams набор средств:

1. Open Visual Studio 2019.
1. Выберите **Расширения Управление**  >  **расширениями**.
1. В поле поиска введите _Teams набор средств_.
1. Выберите расширение Teams набор средств и выберите **Скачать**.

Расширение будет загружено.  Закрыть Visual Studio 2019 г. для установки расширения.

# <a name="command-line"></a>[Командная строка](#tab/cli)

Чтобы установить CLI TeamsFx, используйте диспетчер `npm` пакетов:

``` bash
npm install -g @microsoft/teamsfx-cli
```

В зависимости от конфигурации может потребоваться использовать для `sudo` установки CLI:

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

Это чаще встречается в системах Linux и macOS.

Убедитесь, что вы добавляете глобальный кэш npm в path.  Обычно это делается как часть Node.js установки.  

CLI можно использовать с `teamsfx` командой.  Убедитесь, что команда работает с помощью `teamsfx -h` запуска .

> [!CAUTION]
> Прежде чем запустить TeamsFx в терминалах PowerShell, необходимо включить политику выполнения powerShell с "удаленной подписью".  Дополнительные сведения можно найти в [документации PowerShell.](/powershell/module/microsoft.powershell.core/about/about_signing)

---

## <a name="install-optional-tools"></a>Установка необязательных средств

Установите средства браузера для разработки приложений. Например, если приложение написано с помощью React, вы можете использовать React средства разработчика:

- [React Средства разработчика для Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

Если вы хотите получить доступ к данным, хранимым в Azure, или развернуть облачную Teams приложения в Azure, установите эти средства:

- [Azure Tools для Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [Azure CLI](/cli/azure/install-azure-cli)

Если вы работаете с данными microsoft Graph, вы должны узнать о и закладки Microsoft Graph Explorer. Этот инструмент на основе браузера позволяет запрашивать microsoft Graph за пределами приложения.

- [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)

С помощью портала разработчиков для Teams можно настроить, управлять и распространять приложение Teams (в том числе на ваш сайт или Teams магазин).

- [Портал разработчика для Teams](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a>Включить загрузку побок

Во время разработки необходимо загрузить приложение в течение Teams, не распространяя его.  Это называется "боковой загрузкой".

1. Если у вас есть Teams учетная запись, проверьте, можно ли перегружать приложения в Teams:

    1. В клиенте Teams выберите **Приложения**.
    1. Найди вариант Upload **настраиваемого приложения.**

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, Teams вы можете загрузить пользовательское приложение.":::

> [!NOTE]
> Если вы все еще не можете разгрузить приложения, поговорите с Teams администратором. См. в Teams настраиваемые приложения и [включите настраиваемую загрузку](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) приложений для подробных сведений.

## <a name="get-a-free-teams-developer-tenant-optional"></a>Получите бесплатный клиент Teams разработчика (необязательный)

Если вы не видите параметр sideload или у вас нет учетной записи Teams, вы можете получить бесплатную учетную запись Teams разработчика, присоединившись к программе разработчика M365.  Процесс регистрации занимает примерно две минуты.

1. Перейдите в [Microsoft 365 разработчика](https://developer.microsoft.com/microsoft-365/dev-program).
1. Выберите **Join Now** и следуйте инструкциям на экране.
1. Когда вы доберетсяе до экрана приветствия, выберите **настройка подписки E5**.
1. Настройка учетной записи администратора. Как только вы закончите, вы должны увидеть экран, как это.

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации на программу Microsoft 365 разработчика.":::

1. Войдите Teams с помощью только что настроенной учетной записи администратора.
1. Проверьте, есть ли у **вас Upload настраиваемый параметр** приложения.

## <a name="get-a-free-azure-account"></a>Получить бесплатную учетную запись Azure

Если вы хотите провести свое приложение или получить доступ к ресурсам в Azure, вам потребуется подписка Azure.  Перед [началом работы можно](https://azure.microsoft.com/free/) создать бесплатную учетную запись.

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a>Вход в учетные записи Microsoft 365 Azure

Вам потребуется доступ к двум учетным записям:

- Учетные данные Microsoft 365 учетной записи. Это учетная запись, которую вы используете для регистрации Teams. Если вы используете клиента Microsoft 365 разработчика, это учетная запись администратора, созданная при регистрации программы.
- - Учетные данные Azure. Это учетная запись, используемая для доступа к порталу Azure и для предоставления новых облачных ресурсов для поддержки приложения.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Откройте Visual Studio Code
1. Выберите значок Teams на боковой панели:

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на Visual Studio Code панели.":::

1. Выберите **вход в M365**.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Расположение раздела Учетные записи, используемого для регистрации.":::

1. Процесс регистрации начнется с обычного веб-браузера.  Завершите процесс регистрации для учетной записи M365.  Вам будет предложено закрыть браузер и вернуться к Visual Studio Code.
1. Возвращайся к Teams набор средств в Visual Studio Code.
1. Выберите **вход в Azure.**

    > [!TIP]
    > Если у вас установлено расширение учетной записи Azure и используется та же учетная запись, вы можете пропустить этот шаг.  Вы автоматически будете использовать ту же учетную запись, что и в других расширениях.

1. Процесс регистрации начнется с обычного веб-браузера.  Завершите процесс регистрации для учетной записи Azure.  Вам будет предложено закрыть браузер и вернуться к Visual Studio Code.

По завершению раздел **ACCOUNTS** боковой панели будет показывать две учетные записи отдельно, а также количество доступных для вас подписок Azure.  Убедитесь, что у вас есть по крайней мере одна доступная подписка Azure.  Если нет, выпишитесь и используйте другую учетную запись.

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Visual Studio 2019 г. вы сможете войти в каждую службу по мере необходимости.  Вам не нужно заранее войти в учетные записи M365 и Azure.

# <a name="command-line"></a>[Командная строка](#tab/cli)

1. Во входе Microsoft 365 с CLI TeamsFx:

    ``` bash
    teamsfx account login m365
    ```

    Процесс регистрации начнется с обычного веб-браузера.  Завершите процесс регистрации для учетной записи M365.  Вам будет предложено закрыть браузер.

2. Во входе в Azure с CLI TeamsFx:

    ``` bash
    teamsfx account login azure
    ```

    Процесс регистрации начнется с обычного веб-браузера.  Завершите процесс регистрации для учетной записи Azure.  Вам будет предложено закрыть браузер.

Логины учетных записей делятся между Visual Studio Code и CLI TeamsFx.

---

## <a name="next-steps"></a>Дальнейшие действия

После настройки среды разработки можно создать, создать и развернуть первое Teams приложение.

- [Создайте первое Teams с помощью React](first-app-react.md)
- [Создайте первое Teams приложение с помощью Blazor](first-app-blazor.md)
- [Создайте первое приложение Teams с SharePoint Framework (SPFx)](first-app-spfx.md)
- [Создание приложения-бота для разговоров](first-app-bot.md)
- [Создать расширение для обмена сообщениями](first-message-extension.md)
