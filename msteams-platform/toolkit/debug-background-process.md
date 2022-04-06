---
title: Отладка фоновых процессов
author: zyxiaoyuer
description: Функция Visual Studio Code и набора средств Teams во время локальной отладки
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 74aa3ef53aab329b0b2acae34dc976c142703e0e
ms.sourcegitcommit: 5e5d2d3fb621bcbd9d792a5b450f95167ec8548b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/22/2022
ms.locfileid: "63731892"
---
# <a name="debug-background-process"></a>Отладка фонового процесса

Рабочий процесс локальной отладки включает файлы `.vscode/launch.json` и `.vscode/tasks.json` для настройки отладки в Visual Studio Code. Затем Visual Studio Code запускает отладчики, а отладчик Microsoft Edge или Chrome запускает новый экземпляр браузера следующим образом.

1. Файл `launch.json` настраивает отладчик в Visual Studio Code. 

2. Visual Studio Code выполняет составную команду `preLaunchTask`, `Pre Debug Check & Start All` в файле `.vscode/tasks.json`.

3. Затем Visual Studio Code запускает отладчики, указанные в конфигурациях составной команды, например **Прикрепить к боту**, **Прикрепить к серверу**, **Прикрепить к интерфейсу** и **Запустить бот**.

4.  Отладчик Microsoft Edge или Chrome запускает новый экземпляр браузера и открывает веб-страницу для загрузки клиента Teams.

## <a name="prerequisites"></a>Предварительные требования

Набор средств Teams проверяет указанные ниже предварительные условия в процессе отладки.

* Node.js, применимый для следующих типов проектов.

  |Тип проекта|Версия Node.js LTS|
  |----------|--------------------------------|
  |Вкладка без Функций Azure | 10, 12, **14 (рекомендуется)**, 16 |
  |Вкладка с Функциями Azure | 10, 12, **14 (рекомендуется)**|
  |Bot |  10, 12, **14 (рекомендуется)**, 16|
  |Расширение для обмена сообщениями | 10, 12, **14 (рекомендуется)**, 16 |

   
* Учетная запись Microsoft 365 с действительными учетными данными. Набор средств Teams предлагает вам войти в учетную запись Microsoft 365, если вы не вошли.

* Отправка настраиваемых приложений или загрузка без публикации в вашем клиенте для разработчика включена. Если нет, локальная отладка прекращается.

* Двоичная версия Ngrok 2.3, применимая для бота и расширения обмена сообщениями.  Если Ngrok не установлен или версия не соответствует требованиям, набор средств Teams устанавливает пакет Ngrok NPM `ngrok@4.2.2` в `~/.fx/bin/ngrok`. Двоичная версия Ngrok управляется пакетом Ngrok NPM в `/.fx/bin/ngrok/node modules/ngrok/bin`.

* Azure Functions Core Tools версии 3. Если Azure Functions Core Tools не установлены или версия не соответствует требованиям, набор средств Teams устанавливает пакет NPM Azure Functions Core Tools, azure-functions-core-tools@3 для **Windows** и **macOS** в `~/.fx/bin/func`. Пакет NPM Azure Functions Core Tools в `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` управляет двоичным объектом Azure Functions Core Tools. Для Linux локальная отладка прекращается.

* Версия SDK .NET Core, применимая для Функций Azure. Если SDK .NET Core не установлен или версия не соответствует требованиям, набор средств Teams устанавливает SDK .NET Core для Windows и MacOS в `~/.fx/bin/dotnet`. Для Linux локальная отладка прекращается.

  В следующей таблице перечислены версии .NET Core.

  | Платформа  | Программное обеспечение|
  | --- | --- |
  |Windows, macOS (x64) и Linux | **3.1 (рекомендуется)**, 5.0, 6.0 |
  |macOS (arm64) |6.0 |

* Сертификат разработки. Если сертификат разработки для localhost не установлен для вкладки в Windows или macOS, набор средств Teams предлагает вам установить его.

* Расширения привязок Функций Azure, определенные в `api/extensions.csproj`. Если расширения привязок Функций Azure не установлены, набор средств Teams устанавливает расширения привязок Функций Azure.

* Пакеты NPM, применимые для приложения вкладки, приложения бота, приложения расширения для сообщений и Функций Azure. Если NPM не установлен, набор средств Teams устанавливает все пакеты NPM.

* Бот и расширение для сообщений. Набор средств Teams запускает Ngrok для создания туннеля HTTP для бота и расширения обмена сообщениями.

* Доступные порты. Если порты вкладки, бота, расширения для сообщений и Функций Azure недоступны, локальная отладка прекращается.

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
|Tab without Azure functions | Node.js LTS versions 10, 12, **14 (recommended)**, 16 | The local debug terminates, if Node.js is not installed or the version doesn't match the requirement.|
|Tab with Azure functions | Node.js LTS versions 10, 12, **14 (recommended)** |The local debug terminates, if Node.js is not installed or the version doesn't match the requirement.|
|Bot | Node.js LTS versions 10, 12, **14 (recommended)**, 16|The local debug terminates, if Node.js is not installed or the version doesn't match the requirement.|
|Messaging extension | Node.js LTS versions 10, 12, **14 (recommended)**, 16 |The local debug terminates, if Node.js is not installed or the version doesn't match the requirement.|
|Sign in to Microsoft 365 account | Microsoft 365 credentials |Teams toolkit prompts you to sign in to Microsoft 365 account, if you haven't signed in. |
|Bot, messaging extension | Ngrok version 2.3| • If Ngrok is not installed or the version doesn't match the requirement, the Teams toolkit installs Ngrok NPM package `ngrok@4.2.2` in `~/.fx/bin/ngrok`. </br> • The Ngrok binary is managed by Ngrok NPM package in `/.fx/bin/ngrok/node modules/ngrok/bin`.|
|Azure functions | Azure Functions Core Tools version 3| • If Azure Functions Core Tools is not installed or the version doesn't match the requirement, the Teams toolkit installs Azure Functions Core Tools NPM package, azure-functions-core-tools@3 for **Windows** and for **macOs** in  `~/.fx/bin/func`. </br> • The Azure Functions Core Tools NPM package in  `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` manages Azure Functions Core Tools binary. For Linux, the local debug terminates.|
|Azure functions |.NET Core SDK version|• If .NET Core SDK is not installed or the version  doesn't match the requirement, the toolkit installs .NET Core SDK for Windows and macOS in `~/.fx/bin/dotnet`.</br> • For Linux, the local debug terminates.|
|Azure functions | Azure functions binding extensions defined in `api/extensions.csproj`| If Azure functions binding extensions is not installed, the toolkit installs Azure functions binding extensions.|
|NPM packages| NPM packages for tab app, bot app, messaging extension app, and Azure functions|If NPM is not installed, the toolkit installs all NPM packages.|
|Bot and messaging extension | Ngrok |Toolkit starts Ngrok to create a HTTP tunnel for bot and messaging extension. |

> [!NOTE]
> If tab, bot, messaging extension, and Azure functions ports are unavailable, the local debug terminates.

Use the following .NET Core versions:

| Platform  | Software|
| --- | --- |
|Windows, macOs (x64), Linux | **3.1 (recommended)**, 5.0, 6.0 |
|macOs (arm64) |6.0 |


> [!NOTE]
> If the development certificate for localhost is not installed for tab in Windows or macOS, the Teams toolkit prompts you to install it.</br> -->


Если выбрать **Запуск отладки (F5)**, выходной канал набора средств Teams отображает ход и результат после проверки предварительных требований.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck.png" alt-text="предварительные требования":::

## <a name="register-and-configure-your-teams-app"></a>Регистрация и настройка приложения Teams

В процессе настройки набор средств Teams подготавливает следующие регистрации и конфигурации для вашего приложения Teams.

1. [Регистрирует и настраивает приложение Azure AD](#registers-and-configures-azure-ad-application). Набор средств Teams регистрирует и настраивает ваше приложение Azure AD.

1. [Регистрирует и настраивает бот](#registers-and-configures-bot). Набор средств Teams регистрирует и настраивает ваш бот для вкладки или приложение расширения для сообщений.

1. [Регистрирует и настраивает приложение Teams](#registers-and-configures-teams-app). Набор средств Teams регистрирует и настраивает ваше приложение Teams.

### <a name="registers-and-configures-azure-ad-application"></a>Регистрация и настройка приложения Azure AD

1. Регистрирует приложение Azure AD.

1. Создает секрет клиента.

1. Предоставляет API.

    а. Настраивает URI идентификатора приложения. Для вкладки: `api://localhost/{appId}`. Для бота или расширения обмена сообщениями: `api://botid-{botid}`.

    б. Добавляет область с именем `access_as_user`. Включает ее для **администратора и пользователей**.

В следующей таблице перечислены конфигурации клиентского приложения Microsoft 365 с идентификаторами клиента.

  | Клиентское приложение Microsoft 365 |  Идентификатор клиента  |
  | --- | --- |
  | Классическое, мобильное приложение Teams | 1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
  | Веб-приложение Teams | 5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
  | Office.com | 4345a7b9-9a63-4910-a426-35363201d503 |
  | Office.com | 4765445b-32c6-49b0-83e6-1d93765276ca |
  | Классические приложения Office | 0ec893e0-5785-4de6-99da-4ed124e5296c |
  | Классическое приложение Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
  | Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
  | Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

4. Настраивает разрешения API. Добавляет разрешение Microsoft Graph в **User.Read**.

В следующей таблице перечислены конфигурации проверки подлинности.

  | Тип проекта | URI перенаправления для веб-приложения | URI перенаправления для одностраничного приложения |
  | --- | --- | --- |
  | Tab | `https://localhost:53000/auth-end.html` | `https://localhost:53000/auth-end.html?clientId={appId>}` |
  | Бот или расширение для сообщений | `https://ngrok.io/auth-end.html` | Н/Д |
  
### <a name="registers-and-configures-bot"></a>Регистрация и настройка бота 

Для приложения вкладки или приложения расширения для сообщений:

1. Регистрирует приложение Azure AD.

1. Создает секрет клиента для приложения Azure AD.

1. Регистрирует бота в [Microsoft Bot Framework](https://dev.botframework.com/) с помощью приложения Azure AD.

1. Добавляет канал Microsoft Teams.

1. Настраивает конечную точку обмена сообщениями как `https://{ngrokTunnelId}.ngrok.io/api/messages`.

### <a name="registers-and-configures-teams-app"></a>Регистрация и настройка приложения Teams

Регистрирует приложение Teams на портале [разработчика](https://dev.teams.microsoft.com/home) с помощью шаблона манифеста в `templates/appPackage/manifest.local.template.json`.

После регистрации и настройки приложения создаются файлы локальной отладки.

## <a name="take-a-tour-of-your-app-source-code"></a>Знакомство с исходным кодом приложения

Вы можете просмотреть папки и файлы проекта в области обозревателя Visual Studio Code после того, как набор средств Teams зарегистрирует и настроит ваше приложение. В следующей таблице перечислены файлы локальной отладки и типы конфигурации.

| Имя папки| Содержание| Тип конфигурации отладки |
| --- | --- | --- |
|  `.fx/configs/localSettings.json` | Файл конфигурации локальной отладки | Значения, создаваемые и сохраняемые каждой конфигурацией во время локальной отладки. |
|  `templates/appPackage/manifest.local.template.json` | Файл шаблона манифеста приложения Teams для локальной отладки | Заполнители в файле устраняются во время локальной отладки. |
|  `tabs/.env.teams.local`  | Файл переменных среды для вкладки  | Значения, создаваемые и сохраняемые каждой переменной среды во время локальной отладки. |
|  `bot/.env.teamsfx.local` | Файл переменных среды для бота и расширения обмена сообщениями| Значения, создаваемые и сохраняемые каждой переменной среды во время локальной отладки. |
| `api/.env.teamsfx.local`  | Файл переменных среды для Функций Azure | Значения, создаваемые и сохраняемые каждой переменной среды во время локальной отладки. |


## <a name="see-also"></a>См. также

[Отладка приложения Teams с помощью набора средств Teams](debug-local.md)