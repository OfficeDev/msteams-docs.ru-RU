---
title: Отладка фоновых процессов
author: surbhigupta
description: В этом модуле вы узнаете, как Visual Studio Code и Набор средств Teams работают во время локальной отладки, а также как зарегистрировать и настроить приложение Teams.
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 4d654d5da598b9bf2b9bacfc189c97df08f9a359
ms.sourcegitcommit: 707dad21dc3cf79ac831afe05096c0341bcf2fee
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2022
ms.locfileid: "68653651"
---
# <a name="debug-background-process"></a>Отладка фонового процесса

Процесс локальной отладки включает файлы `.vscode/launch.json` `.vscode/tasks.json` и файлы для настройки отладчика в Microsoft Visual Studio Code. Средство Visual Studio Code запускает отладчики, а Microsoft Edge или Google Chrome запускает новый экземпляр браузера.

Рабочий процесс процесса отладки выглядит следующим образом:

1. `launch.json`Файл  настраивает отладчик в Visual Studio Code.

2. Visual Studio Code запускает составное **приложение preLaunchTask**, **запустите приложение Teams локально** в файле`.vscode/tasks.json`.

3. Затем Visual Studio Code запускает отладчики, указанные в конфигурациях составной команды, например **Прикрепить к боту**, **Прикрепить к серверу**, **Прикрепить к интерфейсу** и **Запустить бот**.

4. Отладчик Microsoft Edge или Google Chrome запускает новый экземпляр браузера и открывает веб-страницу для загрузки клиента Teams.

## <a name="verification-of-prerequisites"></a>Проверка предварительных условий

Набор средств Teams проверяет указанные ниже предварительные условия в процессе отладки.

* Node.js, применимый для следующих типов проектов.

  |Тип проекта|Версия Node.js LTS|
  |----------|--------------------------------|
  |Tab | 14, 16 (рекомендуется) |
  |Вкладка SPFx | 14, 16 (рекомендуется)|
  |Bot |  14, 16 (рекомендуется)|
  |Расширение для сообщений | 14, 16 (рекомендуется) |

* Набор средств Teams предлагает войти в учетную запись Microsoft 365, если вы еще не вошли с действительными учетными данными.
* Пользовательская отправка или загрузка неопубликованных приложений для клиента разработчика включена, чтобы предотвратить завершение локальной отладки.
* Teams Toolkit устанавливает пакет NGROK NPM `ngrok@4.2.2` `~/.fx/bin/ngrok`в том случае, если Ngrok не установлен или версия не соответствует требованиям. Двоичная версия Ngrok 2.3 применима к боту и расширению сообщений. Двоичная версия Ngrok управляется пакетом Ngrok NPM в `/.fx/bin/ngrok/node modules/ngrok/bin`.
* Teams Toolkit устанавливает пакет NPM Функции Azure Core Tools, azure-functions-core-tools@3 для **Windows** и **MacOs**`~/.fx/bin/func`, если Функции Azure Core Tools версии 4 не установлен или версия не соответствует требованиям. Пакет NPM Azure Functions Core Tools в `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` управляет двоичной версией Azure Functions Core Tools. Для Linux локальная отладка прекращается.
* Набор средств Teams устанавливает пакет SDK для .NET Core для **Windows** и **MacOS** `~/.fx/bin/dotnet`в версии пакета SDK для .NET Core, применимой для Функции Azure, если пакет SDK для .NET Core не установлен или версия не соответствует требованиям. Для Linux локальная отладка прекращается.

  В следующей таблице перечислены версии .NET Core.

  | Платформа  | Программное обеспечение|
  | --- | --- |
  |Windows, macOS (x64) и Linux | **3.1 (рекомендуется)**, 5.0, 6.0 |
  |macOS (arm64) |6.0 |

* Если сертификат разработки для localhost не установлен для вкладки **в Windows** или **MacOS**, teams Toolkit предложит установить его.
* Функции Azure расширений `api/extensions.csproj`привязки, определенных в Функции Azure, если расширения привязки не установлены, Teams Toolkit устанавливает Функции Azure привязки.
* Пакеты NPM, применимые для приложения вкладки, приложения бота, приложения расширения для сообщений и Функций Azure. Если пакеты NPM не установлены, Teams Toolkit устанавливает все пакеты NPM.
* Бот и расширение сообщений, Набор средств Teams запускает Ngrok для создания туннеля HTTP для бота и расширения сообщений.
* Доступные порты. Если порты вкладки, бота, расширения сообщений и порты Функций Azure недоступны, локальная отладка прекращается

  В следующей таблице перечислены порты, доступные для компонентов.

  | Компонент  | Порт |
  | --- | --- |
  | Tab | 53000 |
  | Бот или расширение для сообщений | 3978 |
  | Инспектор узла для бота или расширения обмена сообщениями | 9239 |
  | Функции Azure | 7071 |
  | Инспектор узла для Функций Azure | 9229 |

<!-- The following table lists the limitations if the required software is unavailable for debugging:

|Project type|Installation| Limitation|
|----------|--------------------------------|-----|
|Tab without Azure functions | Node.js LTS versions 10, 12, **14 (recommended)**, 16 | The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Tab with Azure functions | Node.js LTS versions 10, 12, **14 (recommended)** |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Bot | Node.js LTS versions 10, 12, **14 (recommended)**, 16|The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Message extension | Node.js LTS versions 10, 12, **14 (recommended)**, 16 |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Sign-in to Microsoft 365 account | Microsoft 365 credentials |Teams Toolkit prompts you to sign-in to Microsoft 365 account, if you haven't signed in. |
|Bot, message extension | Ngrok version 2.3| • If Ngrok isn't installed or the version doesn't match the requirement, the Teams Toolkit installs Ngrok NPM package `ngrok@4.2.2` in `~/.fx/bin/ngrok`. </br> • The Ngrok binary is managed by Ngrok NPM package in `/.fx/bin/ngrok/node modules/ngrok/bin`.|
|Azure functions | Azure Functions Core Tools version 3| • If Azure Functions Core Tools isn't installed or the version doesn't match the requirement, the Teams Toolkit installs Azure Functions Core Tools NPM package, azure-functions-core-tools@3 for **Windows** and for **macOs** in  `~/.fx/bin/func`. </br> • The Azure Functions Core Tools NPM package in `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` manages Azure Functions Core Tools binary. For Linux, the local debug terminates.|
|Azure functions |.NET Core SDK version|• If .NET Core SDK isn't installed or the version  doesn't match the requirement, the Toolkit installs .NET Core SDK for Windows and macOS in `~/.fx/bin/dotnet`.</br> • For Linux, the local debug terminates.|
|Azure functions | Azure functions binding extensions defined in `api/extensions.csproj`| If Azure functions binding extensions isn't installed, the Toolkit installs Azure functions binding extensions.|
|NPM packages| NPM packages for tab app, bot app, message extension app, and Azure functions|If NPM isn't installed, the Toolkit installs all NPM packages.|
|Bot and message extension | Ngrok |Toolkit starts Ngrok to create a HTTP tunnel for bot and message extension. |

> [!NOTE]
> If tab, bot, message extension, and Azure functions ports are unavailable, the local debug terminates.

Use the following .NET Core versions:

| Platform  | Software|
| --- | --- |
|Windows, macOs (x64), Linux | **3.1 (recommended)**, 5.0, 6.0 |
|macOs (arm64) |6.0 |

> [!NOTE]
> If the development certificate for localhost isn't installed for tab in Windows or MacOS, the Teams Toolkit prompts you to install it.</br> -->

Если выбрать **Запуск отладки (F5)**, выходной канал набора средств Teams отображает ход и результат после проверки предварительных требований.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck1.png" alt-text="Сводка по проверке предварительных условий" lightbox="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck1.png":::

## <a name="register-and-configure-teams-app"></a>Регистрация и настройка приложения Teams

В процессе настройки Teams Toolkit подготавливает следующие регистрации и конфигурации для вашего приложения Teams:

1. [Регистрирует и настраивает Microsoft Azure Active Directory (Azure AD)](#registers-and-configures-microsoft-azure-active-directoryazure-ad-app)

1. [Регистрирует и настраивает бот.](#registers-and-configures-bot)

1. [Регистрирует и настраивает приложение Teams](#registers-and-configures-teams-app).

### <a name="registers-and-configures-microsoft-azure-active-directoryazure-ad-app"></a>Регистрирует и настраивает Microsoft Azure Active Directory (Azure AD)

1. Регистрирует Azure AD приложения.

1. Создает секрет клиента.

1. Предоставляет API.

    а. Настраивает URI идентификатора приложения. Для вкладки: `api://localhost/{appId}`. Для бота или расширения для сообщений `api://botid-{botid}`

    б. Добавляет область с именем `access_as_user`. Включает ее для **администратора и пользователей**.

4. Настраивает разрешения API. Добавляет разрешение Microsoft Graph в **User.Read**.

    В следующей таблице перечислены конфигурации проверки подлинности.

      | Тип проекта | URI перенаправления для веб-приложения | URI перенаправления для одностраничного приложения |
      | --- | --- | --- |
      | Tab | `https://localhost:53000/auth-end.html` | `https://localhost:53000/auth-end.html?clientId={appId>}` |
      | Бот или расширение для сообщений | `https://ngrok.io/auth-end.html` | Н/Д |

    В следующей таблице перечислены конфигурации клиентского приложения Microsoft 365 с идентификаторами клиента.

      | Клиентское приложение Microsoft 365 | Идентификатор клиента |
      | --- | --- |
      | Классическое, мобильное приложение Teams | 1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
      | Веб-приложение Teams | 5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
      | Office.com | 4345a7b9-9a63-4910-a426-35363201d503 |
      | Office.com | 4765445b-32c6-49b0-83e6-1d93765276ca |
      | Классические приложения Office | 0ec893e0-5785-4de6-99da-4ed124e5296c |
      | Классическое приложение Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
      | Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
      | Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

### <a name="registers-and-configures-bot"></a>Регистрация и настройка бота

Для приложения вкладки или приложения расширения для сообщений:

1. Регистрирует приложение Azure AD.

1. Создает секрет клиента для приложения Azure AD.

1. Регистрирует бота в [Microsoft Bot Framework](https://dev.botframework.com/) с помощью приложения Azure AD.

1. Добавляет канал Teams.

1. Настраивает конечную точку обмена сообщениями как `https://{ngrokTunnelId}.ngrok.io/api/messages`.

### <a name="registers-and-configures-teams-app"></a>Регистрация и настройка приложения Teams

Регистрирует приложение Teams на [портале разработчика](https://dev.teams.microsoft.com/home) с помощью шаблона манифеста в `templates/appPackage/manifest.template.json`.

После регистрации и настройки приложения создает файлы локальной отладки.

## <a name="take-a-tour-of-your-app-source-code"></a>Знакомство с исходным кодом приложения

Папки и файлы проекта можно просмотреть в **обозревателе** в Visual Studio Code после регистрации и настройки приложения набором средств Teams. В следующей таблице перечислены файлы локальной отладки и типы конфигурации.

| Имя папки| Содержание| Тип конфигурации отладки |
| --- | --- | --- |
|  `.fx/configs/config.local.json` | Файл конфигурации локальной отладки | Значения каждой конфигурации создаются и сохраняются во время локальной отладки. |
|  `templates/appPackage/manifest.template.json` | Файл шаблона манифеста приложения Teams для локальной отладки | Заполнители в файле во время локальной отладки. |
|  `tabs/.env.teams.local`  | Файл переменных среды для вкладки | Значения каждой переменной среды создаются и сохраняются во время локальной отладки. |
|  `bot/.env.teamsfx.local` | Файл переменных среды для бота и расширения для сообщений| Значения каждой переменной среды создаются и сохраняются во время локальной отладки. |
| `api/.env.teamsfx.local`  | Файл переменных среды для Функций Azure | Значения каждой переменной среды создаются и сохраняются во время локальной отладки. |

## <a name="see-also"></a>См. также

* [Отладка приложения Teams с помощью набора средств Teams](debug-local.md)
* [Подготовка облачных ресурсов с помощью набора средств Teams](provision.md)
* [Развертывание в облаке](deploy.md)
* [Предварительный просмотр и настройка манифеста приложения Teams](TeamsFx-preview-and-customize-app-manifest.md)
