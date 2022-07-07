---
title: Интерфейс командной строки TeamsFx
author: MuyangAmigo
description: В этом модуле вы узнаете о библиотеке TeamsFx, интерфейсе командной строки TeamsFx, поддерживаемых командах и их сценариях.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: b3ffa1d6b21ba94dcee9308eba03d4874fca2ba0
ms.sourcegitcommit: 07f41abbeb1572a306a789485953c5588d65051e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/06/2022
ms.locfileid: "66658943"
---
# <a name="teamsfx-library"></a>Библиотека TeamsFx

Microsoft Teams Framework (TeamsFx) — это библиотека, которая инкапсулирует общие функциональные возможности и шаблоны интеграции, такие как упрощенный доступ к удостоверению Майкрософт. Вы можете создавать приложения для Microsoft Teams с нулевой конфигурацией.

Ниже приведен список основных функций TeamsFx.

* **Совместная работа TeamsFx**: позволяет разработчикам и владельцу проекта приглашать других участников совместной работы в проект TeamsFx. Вы можете совместно выполнять отладку и развертывание проекта TeamsFx.

* **CLI TeamsFx**: ускоряет разработку приложений Teams. Он также включает сценарий CI/CD, позволяющий интегрировать интерфейс командной строки в сценарии для автоматизации.

* **Пакет SDK для TeamsFx**: предоставляет доступ к базе данных, например к основной библиотеке кода TeamsFx, содержащей простую проверку подлинности как для клиентского, так и для серверного кода, предназначенного для разработчиков Teams.

## <a name="teamsfx-command-line-interface"></a>Интерфейс командной строки TeamsFx

TeamsFx CLI — это интерфейс командной строки на основе текста, который ускоряет разработку приложений Teams. Он предназначен для обеспечения взаимодействия на основе клавиатуры при создании приложений Teams. Он также включает сценарий CI/CD, позволяющий интегрировать интерфейс командной строки в сценарии для автоматизации.

Дополнительные сведения см. в указанных ниже статьях.

* [Исходный код](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli)
* [Пакет (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>Начало работы

Установите `teamsfx-cli` из `npm` и запустите `teamsfx -h`, чтобы проверить все доступные команды:

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>Поддерживаемые команды

| Команда | Описание |
|----------------|-------------|
| `teamsfx new`| Создание приложения Teams.|
| `teamsfx add`| Добавляет функции в приложение Teams.|
| `teamsfx account`| Управление учетными записями облачных служб. Поддерживаются облачные службы Azure и Microsoft 365. |
| `teamsfx env` | Управление средами. |
| `teamsfx provision` | Подготовка облачных ресурсов в текущем приложении.|
| `teamsfx deploy` | Развертывание текущего приложения.  |
| `teamsfx package` | Сборка приложения Teams в пакет для публикации.|
| `teamsfx validate` | Проверка текущего приложения.|
| `teamsfx publish` | Публикация приложения в Teams.|
| `teamsfx preview` | Предварительный просмотр текущего приложения. |
| `teamsfx config`  | Управление данными конфигурации. |
| `teamsfx permission`| Совместная работа с другими разработчиками в одном проекте.|

## `teamsfx new`

По умолчанию используется `teamsfx new` интерактивный режим и руководства по созданию нового приложения Teams. Вы можете работать в неинтерактивном режиме, заявив `--interactive` для флага значение `false`.

| Команда | Описание |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Создание приложения на основе существующего шаблона |
| `teamsfx new template list`     | Перечисление всех доступных шаблонов |

### <a name="parameters-for-teamsfx-new"></a>Параметры для `teamsfx new`

| Параметр | Требования | Описание |
|:---------------- |:-------------|:-------------|
|`--app-name` | Да| Имя приложения Teams.|
|`--interactive`| Нет | Интерактивный выбор параметров. Варианты: `true` и `false`. Значение по умолчанию — `true`.|
|`--capabilities`| Нет| Выберите возможности приложения Teams, параметры: , , , , , `message-extension``notification`, `search-app``sso-launch-page``command-bot`. `bot``tab-spfx``tab-non-sso``tab` Значение по умолчанию — `tab`.|
|`--programming-language`| Нет| Язык программирования для проекта. Варианты: `javascript` или `typescript`. Значение по умолчанию — `javascript`.|
|`--folder`| Нет | Каталог проекта. В этом каталоге создается вложенная папка с именем вашего приложения. Значение по умолчанию — `./`.|
|`--spfx-framework-type`| Нет| Применимо, если выбрана возможность `SPFx tab`. Интерфейсная платформа. Параметры: `none`и `react` `minimal`, и значение по умолчанию .`none`|
|`--spfx-web part-name`| Нет | Применимо, если выбрана возможность `SPFx tab`. Значение по умолчанию — "helloworld".|
|`--bot-host-type-trigger`| Нет | Применимо, если выбрана возможность `Notification bot`. Доступны следующие параметры: `http-restify`и `timer-functions``http-functions`. Значение по умолчанию — `http-restify`.|

### <a name="scenarios-for-teamsfx-new"></a>Сценарии для `teamsfx new`

Для создания приложения Teams можно использовать интерактивный режим. В следующем списке приведены сценарии управления всеми параметрами с помощью `teamsfx new`:

* Бот уведомлений с триггером HTTP с сервером restify

  ```bash
  teamsfx new --interactive false --capabilities "notification" --bot-host-type-trigger "http-restify" --programming-language "typescript" --folder "./" --app-name       MyAppName
  ```

* Бот команд и ответов Teams

  ```bash
  teamsfx new --interactive false --capabilities "command-bot" --programming-language "typescript" --folder "./" --app-name myAppName
  ```

* Приложение вкладки, размещенное в SPFx с использованием React

  ```bash
  teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
  ```

## `teamsfx add`

В следующей таблице перечислены различные функции приложения Teams, а также их описание.

| Команда | Описание |
|:----------------  |:-------------|
| `teamsfx add notification` | Отправка уведомлений в Microsoft Teams с помощью различных триггеров. |
| `teamsfx add command-and-response` | Отвечать на простые команды в чате Microsoft Teams.|
| `teamsfx add sso-tab` | Веб-страницы с поддержкой удостоверений Teams, внедренные в Microsoft Teams.|
| `teamsfx add tab` | Веб-страницы Hello World, внедренные в Microsoft Teams.|
| `teamsfx add bot` | Чат-бот Hello World для выполнения простых и повторяющихся задач пользователем. |
| `teamsfx add message-extension` | Расширение сообщений Hello World, позволяя выполнять взаимодействия с помощью кнопок и форм. |
| `teamsfx add azure-function`| Бессерверное решение для вычислений на основе событий, позволяющее писать меньше кода. |
| `teamsfx add azure-apim` | Гибридная многооблачная платформа управления для API во всех средах.|
| `teamsfx add azure-sql` | Постоянно актуальные службы реляционных баз данных, созданные для облака. |
| `teamsfx add azure-keyvault` | Облачная служба для безопасного хранения секретов и доступа к ним. |
| `teamsfx add sso` | Разработка функции единого Sign-On для страниц запуска Teams и возможностей бота. |
| `teamsfx add api-connection [auth-type]` | Подключитесь к API с поддержкой проверки подлинности с помощью пакета SDK для TeamsFx. |
| `teamsfx add cicd` | Добавьте рабочие процессы CI/CD для GitHub, Azure DevOps или Jenkins.|

## `teamsfx account`

В следующей таблице перечислены учетные записи облачной службы, такие как Azure и Microsoft 365.

| Команда | Описание |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | Вход в выбранную облачную службу. Варианты обслуживания: Microsoft 365 или Azure. |
| `teamsfx account logout <service>`  | Выход из выбранной облачной службы. Варианты обслуживания: Microsoft 365 или Azure. |
| `teamsfx account set --subscription` | Обновление параметров учетной записи для настройки идентификатора подписки. |

## `teamsfx env`

В следующей таблице перечислены различные среды.

|  Команда  | Описание |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | Добавление новой среды путем копирования из указанной среды. |
| `teamsfx env list` | Перечисление всех сред. |

### <a name="scenarios-for-teamsfx-env"></a>Сценарии для `teamsfx env`

Создайте новую среду путем копирования из существующей среды разработки:

```bash
teamsfx env add staging --env dev
```

## `teamsfx provision`

Подготовка облачных ресурсов в текущем приложении.

| Команда `teamsFx provision` | Описание |
|:----------------  |:-------------|
| `teamsfx provision manifest` | Подготовьте приложение Teams на портале разработчика Teams с соответствующими сведениями, указанными в заданном файле манифеста. |

### <a name="parameters-for-teamsfx-provision"></a>Параметры для `teamsfx provision`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да| Выбор среды для проекта. |
|`--subscription`| Нет | Указание идентификатора подписки Azure. |
|`--resource-group`| Нет | Настройка имени существующей группы ресурсов. |
|`--sql-admin-name`| Нет | Применимо, если в проекте есть ресурс SQL. Имя администратора SQL.|
|`--sql-password`| Нет| Применимо, если в проекте есть ресурс SQL. Пароль администратора SQL.|

## `teamsfx deploy`

Эта команда используется для развертывания текущего приложения. По умолчанию она разворачивает весь проект, но его также можно развернуть частично. Доступны следующие параметры: , , , , , и `spfx``aad-manifest` `manifest`. `bot``apim``function``frontend-hosting`

### <a name="parameters-for-teamsfx-deploy"></a>Параметры для `teamsfx deploy`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да| Выбор существующей среды для проекта. |
|`--open-api-document`| Нет | Применимо, если в проекте есть ресурс APIM. Открытый путь к файлу документа API. |
|`--api-prefix`| Нет | Применимо, если в проекте есть ресурс APIM. Префикс имени API. Уникальное имя по умолчанию для API: `{api-prefix}-{resource-suffix}-{api-version}`. |
|`--api-version`| Нет | Применимо, если в проекте есть ресурс APIM. Версия API. |
|`--include-app-manifest`| Нет | Следует ли развертывать манифест приложения на платформе Teams. Параметры : `yes` и `not`. Значение по умолчанию — `no`. |
|`--include-aad-manifest`| Нет | Указывает, следует ли развертывать манифест AAD. Параметры : `yes` и `not`. Значение по умолчанию — `no`. |

## `teamsfx validate`

Проверка текущего приложения. Эта команда проверяет файл манифеста приложения.

### <a name="parameters-for-teamsfx-validate"></a>Параметры для `teamsfx validate`

`--env`: выбор существующей среды для проекта.

## `teamsfx publish`

Публикация приложения в Teams.

### <a name="parameters-for-teamsfx-publish"></a>Параметры для `teamsfx publish`

`--env`: выбор существующей среды для проекта.

## `teamsfx package`

Сборка приложения Teams в пакет для публикации.

## `teamsfx preview`

Предварительный просмотр текущего приложения из локальной или удаленной среды.

### <a name="parameters-for-teamsfx-preview"></a>Параметры для `teamsfx preview`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--local`| Нет | Предварительный просмотр приложения из локальной среды. `--local` исключает использование `--remote`. |
|`--remote`| Нет | Предварительный просмотр приложения из удаленной среды. `--remote` исключает использование `--local`. |
|`--env`| Нет | Выбор существующей среды для проекта, когда добавлен параметр `--remote`. |
|`--folder`| Нет | Корневой каталог проекта. Значение по умолчанию — `./`. |
|`--browser`| Нет | Браузер для открытия веб-клиента Teams. Варианты: `chrome`, `edge` и `default`, например системный браузер по умолчанию. Значение — `default`. |
|`--browser-arg`| Нет | Аргумент для передачи в браузер. Требует: --browser. Может использоваться несколько раз, например --browser-args="--guest" |
|`--sharepoint-site`| Нет | URL-адрес сайта SharePoint, например `{your-tenant-name}.sharepoint.com` для удаленного предварительного просмотра проекта SPFx. |
|`--m365-host`| Предварительный просмотр приложения в Teams, Outlook или Office. Параметры: `teams`и `office``outlook` . Значение по умолчанию — `teams`. |

### <a name="scenarios-for-teamsfx-preview"></a>Сценарии для `teamsfx preview`

В следующем списке приведены распространенные сценарии для предварительной версии teamsfx:

* Локальный предварительный просмотр

  Зависимости:

  * Node.js
  * Пакет SDK для .NET
  * Azure Functions Core Tools

  ```bash
  teamsfx preview --local
  teamsfx preview --local --browser chrome
  ```

* Удаленный предварительный просмотр

  ```bash
  teamsfx preview --remote
  teamsfx preview --remote --browser edge
  ```

  > [!NOTE]
  > Журналы фоновых служб, например React, сохраняются в `~/.fx/cli-log/local-preview/`.

## `teamsfx config`

Данные конфигурации либо в области пользователя, либо в области проекта.

|  Команда  | Описание |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Просмотр значения конфигурации параметра |
| `teamsfx config set <option> <value>` | Обновление значения конфигурации параметра |

### <a name="parameters-for-teamsfx-config"></a>Параметры для `teamsfx config`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Выбор существующей среды для проекта. |
|`--folder`| Нет | Каталог проекта, используемый для получения или настройки конфигурации проекта. Значение по умолчанию — `./`. |
|`--global`| Нет | Область конфигурации. Если значение равно true, область ограничена областью пользователя, а не областью проекта. Значение по умолчанию — `false`. Теперь поддерживаемые глобальные конфигурации включают `telemetry`, `validate-dotnet-sdk`, `validate-func-core-tools`, `validate-node`. |

### <a name="scenarios-for-teamsfx-config"></a>Сценарии для `teamsfx config`

Секреты в файле `.userdata` шифруются и `teamsfx config` помогают просматривать или обновлять необходимые значения.

* Остановка отправки данных телеметрии

  ```bash
  teamsfx config set telemetry off
  ```

* Отключение средства проверки среды

  Существует три конфигурации для включения или отключения Node.js, .NET SDK и Функции Azure Core Tools, и все они включены по умолчанию. Если вам не нужна проверка зависимостей и вы хотите установить зависимости самостоятельно, можно установить для конфигурации значение "off". Ознакомьтесь со следующими руководствами.

  * [Руководство по установке Node.js](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
  * [Руководство по установке пакета SDK для .NET](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
  * [Функции Azure по установке Core Tools](<https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure>- functions-core-tools).

  Чтобы отключить проверку пакета SDK для .NET, вы можете использовать следующую команду.

  ```bash
  teamsfx config set validate-dotnet-sdk off
  ```

  Чтобы включить проверку пакета SDK для .NET, вы можете использовать следующую команду.

  ```bash
  teamsfx config set validate-dotnet-sdk on
  ```

* Просмотр всей конфигурации области пользователя

  ```bash
  teamsfx config get -g
  ```

* Просмотр всей конфигурации в проекте

  Секрет расшифровывается автоматически:

    ```bash
    teamsfx config get --env dev
    ```

* Обновление конфигурации секрета в проекте

  ```bash
  teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
  ```

## `teamsfx permission`

TeamsFx CLI предоставляет `teamsFx permission` команды для сценариев совместной работы.

|  Команды | Описание |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | Предоставление разрешения для учетной записи Microsoft 365 участника совместной работы для проекта указанной среды. |
| `teamsfx permission status` | Отображение состояния разрешений для проекта |

### <a name="parameters-for-teamsfx-permission-grant"></a>Параметры для `teamsfx permission grant`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Указание имени среды. |
|`--email`| Да | Указание адреса электронной почты Microsoft 365 участника совместной работы. Убедитесь, что учетная запись участника совместной работы находится в одном клиенте с создателем. |

### <a name="parameters-for-teamsfx-permission-status"></a>Параметры для `teamsfx permission status`

| Параметр | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Указание имени среды. |
|`--list-all-collaborators` | Нет | С помощью этого флага CLI набора средств Teams печатает всех участников совместной работы для этого проекта. |

### <a name="scenarios-for-teamsfx-permission"></a>Сценарии для `teamsfx permission`

Следующий список предоставляет необходимые разрешения для `TeamsFx` проектов:

* Предоставление разрешения

  Создатель проекта и участники совместной работы могут использовать команду `teamsfx permission grant` для добавления нового участника совместной работы в проект:

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  Получив необходимое разрешение, создатель проекта и участники совместной работы могут предоставить общий доступ к проекту новому участнику совместной работы с помощью GitHub, а новый участник совместной работы может иметь все разрешения для учетной записи Microsoft 365.

* Отображение состояния разрешения

  Создатель проекта и участники совместной `teamsfx permission status` работы могут использовать команду для просмотра разрешений учетной записи Microsoft 365 для определенной env:

  ```bash
  teamsfx permission status --env dev
  ```

* Перечисление всех участников совместной работы

  Автор проекта и участники совместной работы могут использовать команду `teamsfx permission status` для просмотра всех участников совместной работы для конкретной среды:

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

* Рабочий процесс совместной работы E2E в CLI

  * Как создатель проекта:

    * Чтобы создать проект бота или вкладки TeamsFx и выбрать Azure в качестве типа узла:

      ```bash
      teamsfx new --interactive false --app-name newapp --host-type azure
      ```

    * Чтобы войти в учетную запись Microsoft 365 и учетную запись Azure, выполните следующие действия.

      ```bash
      teamsfx account login azure
      teamsfx account login Microsoft 365
      ```

    * Чтобы подготовить проект:

      ```bash
      teamsfx provision
      ```

    * Чтобы просмотреть участников совместной работы:

      ```bash
      teamsfx permission status --env dev --list-all-collaborators
      ```

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-status-all-1.png" alt-text="permission-1":::

    * Чтобы добавить другую учетную запись в качестве участника совместной работы. Убедитесь, что добавленная учетная запись находится в том же клиенте:

      ```bash
      teamsfx permission grant --env dev --email user-email@user-tenant.com
      ```

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="permission":::

    * Чтобы отправить проект в GitHub

  * Как участник совместной работы над проектом:

    * Клонируйте проект из GitHub.
    * Войдите в учетную запись Microsoft 365. Убедитесь, что добавлена та же учетная запись Microsoft 365:

      ```bash
      teamsfx account login Microsoft 365
      ```

    * Войдите в учетную запись Azure с разрешением участника для всех ресурсов Azure.

      ```bash
      teamsfx account login azure
      ```

    * Проверьте состояние разрешения. У вас должно быть разрешение владельца проекта:

      ```bash
      teamsfx permission status --env dev
      ```

      ![состояние разрешения](./images/permission-status.png)

    * Обновите код вкладки и разверните проект в удаленной среде.
    * Запустите в удаленном режиме. Проект должен работать нормально.

## <a name="deploy-to-azure-web-app-manually"></a>Развертывание в веб-приложении Azure вручную

1. Создайте вкладку включения единого входа.
2. Подготовьте проект:

      ```bash
      teamsfx provision
      ```

3. Запуск `npm install` и `npm run build:teamsfx:dev` установка `tabs` добавленных `api folder` пакетов.

4. Создайте службу приложений Windows (ту же ОС на компьютере).

5. Выполните `$ az webapp up --name --html --subscription` или `build` `tabs` .`folder`

6. Измените `templates/azure/provision/frontendHosting.bicep`.

7. Снова подготовься. Набор средств Teams обновляет Azure Active Directory и манифест для вас.

8. Найдите свою `appPackage.dev.zip` папку сборки или AppPackage и добавьте ее в Teams.

## <a name="see-also"></a>Дополнительные ресурсы

* [Пакет SDK TeamsFx для TypeScript или JavaScript](TeamsFx-SDK.md)
* [Управление несколькими средами в наборе средств Teams](TeamsFx-multi-env.md)
* [Совместная работа над проектом Teams с помощью набора средств Teams](TeamsFx-collaboration.md)
* [Общие сведения о наборе средств Teams](teams-toolkit-fundamentals.md)
