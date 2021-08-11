---
title: Начало работы - Необходимые условия
author: adrianhall
description: Узнайте, как начать работу с разработкой Microsoft Teams и настроить среду.
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 82b4c6b54286f70672fecd0f5dd059cf7f47036821b078d502ba9cae73dc5498
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2021
ms.locfileid: "57703166"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a>Необходимые условия: начало разработки Microsoft Teams приложения

Прежде чем приступить к созданию первого Teams приложения, необходимо установить несколько инструментов и настроить среду разработки.

## <a name="install-required-tools"></a>Установка необходимых средств

Некоторые из необходимых инструментов зависят от того, как вы предпочитаете создавать Teams приложение:

- [Node.js](https://nodejs.org/en/download/) (используйте последний выпуск V14 LTS)
- Браузер с средствами разработки, такими как [Microsoft Edge](https://www.microsoft.com/edge) (рекомендуется) или [Google Chrome](https://www.google.com/chrome/)
- Если вы разрабатываете с Помощью JavaScript, TypeScript или SharePoint Framework (SPFx), установите Visual Studio Code [версии](https://code.visualstudio.com/download)1.55 или более поздней версии.  
- Если вы разрабатываете с помощью .NET, [установите Visual Studio 2019](https://visualstudio.com/download). Убедитесь, что ASP.NET **и веб-разработки** или **межплатформеной** рабочей нагрузки .NET Core.

> [!WARNING]
> Известны проблемы с пакетом `npm@7` с node v15 и более поздним пакетом. Если у вас возникли проблемы с запуском, убедитесь, что `npm install` вы используете узел v14 (LTS)

## <a name="install-the-teams-toolkit"></a>Установка Teams набор средств

Этот Teams набор средств упрощает процесс разработки с помощью средств для обеспечения и развертывания облачных ресурсов для приложения, публикации в Teams магазине и других. Инструментарий можно использовать с помощью Visual Studio Code, Visual Studio или CLI `teamsfx` (называется). Дополнительные сведения см. [в Teams набор средств для Visual Studio Code](../toolkit/visual-studio-code-overview.md), Teams набор средств для [Visual Studio](../toolkit/visual-studio-overview.md) и [средства CLI Teamsfx](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli).

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Откройте Visual Studio Code.
1. Выберите представление **Расширения** **(Ctrl+Shift+X**  /  **⌘⇧-X** или **> расширения).**
1. В поле поиска введите **Teams набор средств**.
1. Выберите **Установите** рядом с Teams набор средств.

Вы также можете найти Teams набор средств на Visual Studio Code [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

Следующие средства могут быть установлены расширением Visual Studio Code при необходимости. Если уже установлено, установленную версию можно использовать вместо нее. Если используется Linux, включая WSL, необходимо установить эти средства перед использованием:

- [Основные средства Azure Functions](/azure/azure-functions/functions-run-local)

    Основные средства Azure Functions используются для локального запуска отлаженных компонентов, включая помощников проверки подлинности, необходимых при запуске служб в Azure. Он устанавливается в каталоге проекта (с помощью `devDependencies` npm).

- [SDK .NET](/dotnet/core/install/)

    SDK .NET используется для установки настраиваемых привязки для локального отладки и развертывания приложений Azure Functions. Если вы не установили SDK .NET 3.1 (или более поздней версии) глобально, портативная версия может быть установлена.

- [ngrok](https://ngrok.com/download)

    Некоторые Teams приложения (беседные боты, расширения обмена сообщениями и входящие веб-оки) требуют входящих подключений. Необходимо подвергать систему разработки Teams через туннель. Туннель не требуется для приложений, которые включают только вкладки. Этот пакет устанавливается в каталоге проекта (с помощью `devDependencies` npm).

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Вы можете использовать Visual Studio 2019 для разработки Teams с помощью Blazor Server в .NET. Если вы не собираетесь разрабатывать Teams в .NET, установите Visual Studio Code версию Teams набор средств.

Чтобы установить расширение Teams набор средств:

1. Open Visual Studio 2019.
1. Выберите **Расширения Управление**  >  **расширениями**.
1. В поле поиска введите **Teams набор средств**.
1. Выберите расширение Teams набор средств и выберите **Скачать**. Расширение загружается.
1. Закрыть Visual Studio 2019 г. для установки расширения.

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

Убедитесь, что вы добавляете глобальный кэш npm в path. Обычно это делается как часть Node.js установки.  

CLI можно использовать с `teamsfx` командой. Убедитесь, что команда работает с помощью `teamsfx -h` запуска .

> [!CAUTION]
> Прежде чем запустить TeamsFx в терминалах PowerShell, необходимо включить политику "удаленного подписанного" выполнения для PowerShell. Дополнительные сведения можно найти в [документации PowerShell.](/powershell/module/microsoft.powershell.core/about/about_signing)

---

## <a name="install-optional-tools"></a>Установка необязательных средств

Установите средства браузера для разработки приложений. Например, если приложение написано с помощью React, вы можете использовать React средства разработчика:

- [React Средства разработчика для Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

Если вы хотите получить доступ к данным, хранимым в Azure, или развернуть облачную Teams приложения в Azure, установите эти средства:

- [Azure Tools для Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [Azure CLI](/cli/azure/install-azure-cli)

Если вы работаете с данными microsoft Graph, вы должны узнать о и закладки Microsoft Graph Explorer. Этот инструмент на основе браузера позволяет запрашивать microsoft Graph за пределами приложения.

- [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)

С помощью портала разработчиков для Teams вы можете настроить, управлять и распространять Teams приложения, в том числе в организации или Teams магазине.

- [Портал разработчиков Teams](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a>Включить загрузку побок

Во время разработки необходимо загрузить приложение в пределах Teams без его распространения. Это называется боковой загрузкой.

Если у вас есть Teams учетная запись, проверьте, можно ли перегружать приложения в Teams:

1. В клиенте Teams выберите **Приложения**.
1. Выберите **Upload настраиваемом приложении.**

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, Teams вы можете загрузить пользовательское приложение.":::

> [!NOTE]
> Если вы по-прежнему не можете разгрузить приложения, поговорите с Teams администратором. См. в Teams настраиваемые приложения и [включите настраиваемую загрузку](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) приложений для подробных сведений.

## <a name="get-a-free-teams-developer-tenant-optional"></a>Получите бесплатный клиент Teams разработчика (необязательный)

Если вы не видите параметр sideload или у вас нет учетной записи Teams, вы можете получить бесплатную учетную запись Teams разработчика, присоединившись к программе разработчика M365.  Процесс регистрации занимает примерно две минуты.

1. Перейдите в [Microsoft 365 разработчика](https://developer.microsoft.com/microsoft-365/dev-program).
1. Выберите **Join Now** и следуйте инструкциям на экране.
1. На экране приветствия выберите **настройка подписки E5.**
1. Настройка учетной записи администратора. После завершения, вы должны увидеть экран, как это.

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации на программу Microsoft 365 разработчика.":::

1. Вопишитесь Teams с помощью только что настроенной учетной записи администратора. Убедитесь, что у **Upload есть настраиваемый параметр** приложения.

## <a name="get-a-free-azure-account"></a>Получить бесплатную учетную запись Azure

Если вы хотите провести свое приложение или получить доступ к ресурсам в Azure, необходимо иметь подписку Azure.  Перед [началом работы можно](https://azure.microsoft.com/free/) создать бесплатную учетную запись.

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a>Вход в учетные записи Microsoft 365 Azure

Необходимо иметь доступ к двум учетным записям:

- Учетные данные Microsoft 365 учетной записи. Это учетная запись, которую вы используете для регистрации Teams. Если вы используете клиента Microsoft 365 разработчика, это учетная запись администратора, настроенная при регистрации для программы.
- Учетные данные Azure. Это учетная запись, используемая для доступа к порталу Azure и для предоставления новых облачных ресурсов для поддержки приложения.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Откройте Visual Studio Code
1. Выберите значок Teams на боковой панели:

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. Выберите **вход в M365**.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Расположение раздела Учетные записи, используемого для регистрации.":::

    Процесс регистрации начинается с обычного веб-браузера. Завершите процесс регистрации для учетной записи M365. При запросе можно закрыть браузер и вернуться к Visual Studio Code.
1. Возвращайся к Teams набор средств в Visual Studio Code.
1. Выберите **вход в Azure.**

    > [!TIP]
    > Если у вас установлено расширение учетной записи Azure и используется та же учетная запись, вы можете пропустить этот шаг. Используйте ту же учетную запись, что и в других расширениях.

1. Процесс регистрации начинается с обычного веб-браузера.  Завершите процесс регистрации для учетной записи Azure. При запросе можно закрыть браузер и вернуться к Visual Studio Code.

    По завершению раздел **ACCOUNTS** боковой панели отображает две учетные записи отдельно, а также количество доступных вам подписок Azure. Убедитесь, что у вас есть по крайней мере одна доступная подписка Azure. Если нет, выпишитесь и используйте другую учетную запись.

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Visual Studio 2019 г. при необходимости необходимо войти в каждую службу. Вам не нужно заранее войти в учетные записи M365 и Azure.

# <a name="command-line"></a>[Командная строка](#tab/cli)

1. Во входе Microsoft 365 с CLI TeamsFx:

    ``` bash
    teamsfx account login m365
    ```

    Процесс регистрации начинается с обычного веб-браузера. Завершите процесс регистрации для учетной записи M365. Вам будет предложено закрыть браузер.

2. Во входе в Azure с CLI TeamsFx:

    ``` bash
    teamsfx account login azure
    ```

    Процесс регистрации начинается с обычного веб-браузера. Завершите процесс регистрации для учетной записи Azure. Вам будет предложено закрыть браузер.

    Логины учетных записей делятся между Visual Studio Code и CLI TeamsFx.



    После настройки среды разработки можно создать, создать и развернуть первое Teams приложение.

## <a name="see-also"></a>См. также

* [Обзор учебников](code-samples.md) 
* [Создание приложения с React](first-app-react.md)
* [Создание приложения с помощью Blazor](first-app-blazor.md)
* [Создание приложения с SPFx](first-app-spfx.md)
* [Создание приложения с помощью C# или .NET](get-started-dotnet-app-studio.md)
* [Создайте приложение с помощью Node.js](get-started-nodejs-app-studio.md)
* [Создание приложения с помощью генератора Yeoman](get-started-yeoman.md)
* [Создание бота беседы](first-app-bot.md)
* [Создание расширения для обмена сообщениями](first-message-extension.md)
* [Примеры кода](https://github.com/OfficeDev/Microsoft-Teams-Samples)
