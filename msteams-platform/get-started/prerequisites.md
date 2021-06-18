---
title: Начало работы - Необходимые условия
author: adrianhall
description: Узнайте, как начать работу с разработкой приложения Microsoft Teams и настроить среду.
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 6496d238b3858c1df974732fa57c28eed7c54eb2
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994191"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a>Необходимые условия: начало разработки приложения Microsoft Teams

Перед созданием первого приложения Teams необходимо установить несколько инструментов и настроить среду разработки.

## <a name="install-required-tools"></a>Установка необходимых средств

Некоторые из необходимых инструментов зависят от того, как вы предпочитаете создавать приложение Teams:

- [Node.js](https://nodejs.org/en/download/) (используйте последний выпуск V14 LTS)
- Браузер с средствами разработчика , такими как [Microsoft Edge](https://www.microsoft.com/edge) (рекомендуется) или [Google Chrome](https://www.google.com/chrome/)
- Если вы разрабатываете с помощью JavaScript, TypeScript или SharePoint Framework (SPFx), установите код Visual Studio [версии](https://code.visualstudio.com/download)1.55 или более поздней версии.  
- Если вы разрабатываете с помощью .NET, [установите Visual Studio 2019](https://visualstudio.com/download). Убедитесь, что ASP.NET **и веб-разработки** или **межплатформеной** рабочей нагрузки .NET Core.

> [!WARNING]
> Известны проблемы с пакетом `npm@7` с node v15 и более поздним пакетом. Если у вас возникли проблемы с запуском, убедитесь, что `npm install` вы используете узел v14 (LTS)

## <a name="install-the-teams-toolkit"></a>Установка команд набор средств

Командная набор средств упрощает процесс разработки с помощью средств для обеспечения и развертывания облачных ресурсов для приложения, публикации в магазине Teams и других. Инструментарий можно использовать с Visual Studio кодом, Visual Studio или CLI `teamsfx` (называется).

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Откройте Visual Studio Code.
1. Выберите представление Расширения **(Ctrl+Shift+X**  /  **⌘⇧-X** или **> расширения).**
1. В поле поиска введите **Teams набор средств**.
1. Выберите зеленую кнопку установки рядом с командой набор средств.

Вы также можете найти командные набор средств на Visual Studio [Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

Следующие средства могут быть установлены расширением Visual Studio кода, когда они необходимы. Если уже установлено, установленную версию можно использовать вместо нее. Если используется Linux, включая WSL, необходимо установить эти средства перед использованием:

- [Основные средства Azure Functions](/azure/azure-functions/functions-run-local)

    Основные средства Azure Functions используются для локального запуска отлаженных компонентов, включая помощников проверки подлинности, необходимых при запуске служб в Azure. Он устанавливается в каталоге проекта (с помощью `devDependencies` npm).

- [SDK .NET](/dotnet/core/install/)

    SDK .NET используется для установки настраиваемых привязки для локального отладки и развертывания приложений Azure Functions. Если вы не установили SDK .NET 3.1 (или более поздней версии) глобально, портативная версия может быть установлена.

- [ngrok](https://ngrok.com/download)

    Некоторые функции приложения Teams (беседующие боты, расширения обмена сообщениями и входящие веб-окки) требуют входящих подключений. Вам необходимо выставить систему разработки в Teams через туннель. Туннель не требуется для приложений, которые включают только вкладки. Этот пакет устанавливается в каталоге проекта (с помощью `devDependencies` npm).

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Вы можете использовать Visual Studio 2019 г. для разработки приложений Teams с помощью Blazor Server в .NET. Если вы не собираетесь разрабатывать приложения Teams в .NET, установите Visual Studio код teams набор средств.

Чтобы установить расширение Teams набор средств:

1. Open Visual Studio 2019.
1. Выберите **Расширения Управление**  >  **расширениями**.
1. В поле поиска введите **Teams набор средств**.
1. Выберите расширение Teams набор средств и выберите **Скачать**.

Расширение можно скачать. Закрыть Visual Studio 2019 г. для установки расширения.

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

Установите средства браузера для разработки приложений. Например, если приложение написано с React, вы можете использовать средства разработчика React:

- [React Developer Tools for Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

Если вы хотите получить доступ к данным, хранимым в Azure, или развернуть облачный backend для приложения Teams в Azure, установите эти средства:

- [Azure Tools для Visual Studio кода](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [Azure CLI](/cli/azure/install-azure-cli)

Если вы работаете с данными Microsoft Graph, вы должны узнать о и закладки обозревателя Microsoft Graph. Этот инструмент на основе браузера позволяет запрашивать Microsoft Graph вне приложения.

- [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)

На портале разработчиков для teams можно настроить, управлять и распространять приложение Teams, в том числе в организации или магазине Teams.

- [Портал разработчиков Teams](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a>Включить загрузку побок

Во время разработки необходимо загрузить приложение в Teams, не распространяя его. Это называется "боковой загрузкой".

1. Если у вас есть учетная запись Teams, убедитесь, что вы можете разгрузить приложения в Teams:

    1. В клиенте Teams выберите **Приложения.**
    1. Найди вариант **для загрузки настраиваемого приложения.**

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, где в Teams можно загрузить настраиваемые приложения.":::

> [!NOTE]
> Если вы по-прежнему не можете разгрузить приложения, поговорите с администратором Teams. Включите настраиваемые приложения Teams и [включите настраиваемую загрузку приложений](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) для подробных сведений.

## <a name="get-a-free-teams-developer-tenant-optional"></a>Получить бесплатного клиента разработчика Teams (необязательный)

Если вы не видите параметр sideload или у вас нет учетной записи Teams, вы можете получить бесплатную учетную запись разработчика Teams, присоединившись к программе разработчика M365.  Процесс регистрации занимает примерно две минуты.

1. Перейдите к [программе разработчика Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)
1. Выберите **Join Now** и следуйте инструкциям на экране.
1. Когда вы доберетсяе до экрана приветствия, выберите **настройка подписки E5**.
1. Настройка учетной записи администратора. Как только вы закончите, вы должны увидеть экран, как это.

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации на программу разработчика Microsoft 365.":::

1. Вопишите в Teams с помощью только что настроенной учетной записи администратора.
1. Убедитесь, что теперь у вас есть **настраиваемый параметр Upload приложения.**

## <a name="get-a-free-azure-account"></a>Получить бесплатную учетную запись Azure

Если вы хотите провести свое приложение или получить доступ к ресурсам в Azure, необходимо иметь подписку Azure.  Перед [началом работы можно](https://azure.microsoft.com/free/) создать бесплатную учетную запись.

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a>Вход в учетные записи Microsoft 365 и Azure

Необходимо иметь доступ к двум учетным записям:

- Учетные данные учетных записей Microsoft 365. Это учетная запись, которую вы используете для регистрации в Teams. Если вы используете клиента программы разработчика Microsoft 365, это учетная запись администратора, созданная при регистрации для программы.
- - Учетные данные Azure. Это учетная запись, используемая для доступа к порталу Azure и для предоставления новых облачных ресурсов для поддержки приложения.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Open Visual Studio Code
1. Выберите значок Teams на боковой панели:

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. Выберите **вход в M365**.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Расположение раздела Учетные записи, используемого для регистрации.":::

1. Процесс регистрации начинается с обычного веб-браузера. Завершите процесс регистрации для учетной записи M365. Вам будет предложено закрыть браузер и вернуться к Visual Studio Code.
1. Возвращайся к Teams набор средств в Visual Studio Code.
1. Выберите **вход в Azure.**

    > [!TIP]
    > Если у вас установлено расширение учетной записи Azure и используется та же учетная запись, вы можете пропустить этот шаг. Используйте ту же учетную запись, что и в других расширениях.

1. Процесс регистрации начинается с обычного веб-браузера.  Завершите процесс регистрации для учетной записи Azure. Вам будет предложено закрыть браузер и вернуться к Visual Studio Code.

По завершению раздел **ACCOUNTS** боковой панели отображает две учетные записи отдельно, а также количество доступных вам подписок Azure. Убедитесь, что у вас есть по крайней мере одна доступная подписка Azure. Если нет, выпишитесь и используйте другую учетную запись.

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

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

---

После настройки среды разработки можно создать, создать и развернуть первое Teams приложение.

## <a name="see-also"></a>См. также

- [Создайте первое Teams приложение с помощью Blazor](first-app-blazor.md)
- [Создайте первое приложение Teams с SharePoint Framework (SPFx)](first-app-spfx.md)
- [Создание бота беседы](first-app-bot.md)
- [Создание расширения для обмена сообщениями](first-message-extension.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создайте первое Teams с помощью React](first-app-react.md)
