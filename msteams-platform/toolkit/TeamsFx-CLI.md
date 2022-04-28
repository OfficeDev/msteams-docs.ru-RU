---
title: Интерфейс командной строки TeamsFx
author: MuyangAmigo
description: Описание интерфейса командной строки TeamsFx
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 5fde7e94c198bfe76810a52ede78d0be7270ba0c
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104520"
---
# <a name="teamsfx-library"></a>Библиотека TeamsFx

Microsoft Teams Framework (TeamsFx) — это библиотека, которая инкапсулирует общие функциональные возможности и шаблоны интеграции (например, упрощенный доступ к Удостоверению Майкрософт). Вы можете создавать приложения для Microsoft Teams с нулевой конфигурацией.

Ниже приведен список основных функций TeamsFx.

* **Совместная работа TeamsFx**: разрешить разработчикам и владельцу проекта приглашать других участников совместной работы в проект TeamsFx. Вы можете совместно выполнять отладку и развертывание проекта TeamsFx.

* **TeamsFx CLI**: он ускоряет Teams разработки приложений. Он также включает сценарий CI/CD, в котором можно интегрировать интерфейс командной строки в скрипты для автоматизации.

* **Пакет SDK для TeamsFx**: пакет SDK для TeamsFx — это основная библиотека кода TeamsFx, которая инкапсулирует простую проверку подлинности как для клиентского, так и для серверного кода, предназначенного для Teams разработчиков.

## <a name="teamsfx-command-line-interface"></a>Интерфейс командной строки TeamsFx

TeamsFx CLI — это текстовый интерфейс командной строки, который ускоряет Teams приложений. Она предназначена для обеспечения взаимодействия с клавиатурой при создании Teams приложений. Он также включает сценарий CI/CD, в котором можно интегрировать интерфейс командной строки в скрипты для автоматизации.

Дополнительные сведения см. в указанных ниже статьях.

* [Исходный код](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli)
* [Пакет (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>Начало работы

Установите `teamsfx-cli` и `npm` запустите, `teamsfx -h` чтобы проверить все доступные команды:

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>Поддерживаемые команды

| Команда | Описание |
|----------------|-------------|
| `teamsfx new`| Создайте новое Teams приложения.|
| `teamsfx account`| Управление учетными записями облачных служб. Поддерживаются облачные службы Azure и Microsoft 365. |
| `teamsfx env` | Управление средами. |
| `teamsfx capability`| Добавьте новые возможности в текущее приложение.|
| `teamsfx resource`  | Управление ресурсами в текущем приложении.|
| `teamsfx provision` | Подготовка облачных ресурсов в текущем приложении.|
| `teamsfx deploy` | Разверните текущее приложение.  |
| `teamsfx package` | Создайте Teams приложения в пакет для публикации.|
| `teamsfx validate` | Проверьте текущее приложение.|
| `teamsfx publish` | Опубликуйте приложение в Teams.|
| `teamsfx preview` | Предварительный просмотр текущего приложения. |
| `teamsfx config`  | Управление данными конфигурации. |
| `teamsfx permission`| Совместная работа с другими разработчиками в одном проекте.|

## `teamsfx new`

По умолчанию переходит `teamsfx new` в интерактивный режим и описывает процесс создания нового Teams приложения. Вы также можете работать с неинтерактивным режимом, заявив `--interactive` для флага значение `false`.

| `teamsFx new` Команды | Описание |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Создание приложения на основе существующего шаблона |
| `teamsfx new template list`     | Вывод списка всех доступных шаблонов |

### <a name="parameters-for-teamsfx-new"></a>Параметры для `teamsfx new`

| Параметр | Требования | Описание |
|:---------------- |:-------------|:-------------|
|`--app-name` | Да| Имя Teams приложения.|
|`--interactive`| Нет | Выберите параметры в интерактивном режиме. Параметры доступны, `true` а `false` значение по умолчанию — . `true`.|
|`--capabilities`| Нет| Выберите Teams приложения, несколько вариантов: `tab`и `bot``messaging-extension` `tab-spfx`. Значение по умолчанию — `tab`.|
|`--programming-language`| Нет| Язык программирования для проекта. Параметры имеют значение или `javascript` значение `typescript` по умолчанию `javascript`.|
|`--folder`| Нет | Project каталога. В этом каталоге создается вложенная папка с именем вашего приложения. Значение по умолчанию — `./`.|
|`--spfx-framework-type`| Нет| Применимо, если `Tab(SPfx)` выбрана возможность. Frontend Framework. Доступны параметры и `none` `react`значение по умолчанию `none`.|
|`--spfx-web part-name`| Нет | Применимо, если `Tab(SPfx)` выбрана возможность. Значение по умолчанию — helloworld.|
|`--spfx-web part-desp`| Нет | Применимо, если `Tab(SPfx)` выбрана возможность. Значение по умолчанию — helloworld description. |
|`--azure-resources`| Нет| Применимо, если содержит `tab` возможность. Добавьте ресурсы Azure в проект. Несколько вариантов: `sql` (База данных SQL Azure) и `function` (Функции Azure). |

### <a name="scenarios-for-teamsfx-new"></a>Сценарии для `teamsfx new`

Вы можете использовать интерактивный режим для создания Teams приложения. Ниже приведены сценарии управления всеми параметрами`teamsfx new`.

#### <a name="tab-app-hosted-on-spfx-using-react"></a>Приложение tab, размещенное на SPFx с помощью React

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>Teams в JavaScript с вкладкой, возможностями бота и Функции Azure

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>Teams вкладки с Функции Azure и Azure SQL

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

Управление учетными записями облачных служб. Поддерживаются облачные службы и `Azure` `Microsoft 365`.

| `teamsFx account` Команды | Описание |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | Войдите в выбранную облачную службу. |
| `teamsfx account logout <service>`  | выйдите из выбранной облачной службы. |
| `teamsfx account set --subscription` | Обновим параметры учетной записи, чтобы задать идентификатор подписки. |

## `teamsfx env`

Управление средами.

| `teamsfx env` Команды  | Описание |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | Добавьте новую среду путем копирования из указанной среды. |
| `teamsfx env list` | Вывод списка всех сред. |

### <a name="scenarios-for-teamsfx-env"></a>Сценарии для `teamsfx env`

Ниже приведены сценарии `teamsfx env` .

#### <a name="create-a-new-environment"></a>Создание среды

Добавьте новую среду путем копирования из существующей среды разработки:

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

Добавьте новые возможности в текущее приложение.

| `teamsFx capability` Команды  | Описание |
|:----------------  |:-------------|
| `teamsfx capability add tab` | Добавление вкладки |
| `teamsfx capability add bot` | Добавление бота |
| `teamsfx capability add messaging-extension`| Добавление расширения messagE |

> [!NOTE]
> Если проект содержит бот, расширение сообщения невозможно добавить, и оно применяется наоборот. Вы можете включить в проект расширения ботов и сообщений при создании нового Teams приложения.

## `teamsfx resource`

Управление ресурсами в текущем приложении. Поддерживаются `<resource-type>` следующие: `azure-sql`и `azure-apim` `azure-function` .

| `teamsFx resource` Команды  | Описание |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | Добавьте ресурс в текущее приложение.|
| `teamsfx resource show <resource-type>`      | Отображение сведений о конфигурации ресурса. |
| `teamsfx resource list`      | Выведите список всех ресурсов в текущем приложении. |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>Параметры для `teamsfx resource add azure-function`

| Параметр  | Требования | Описание |
|----------------  |-------------|-------------|
|`--function-name`| Да | Укажите имя функции. Значение по умолчанию — `getuserprofile`. |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>Параметры для `teamsfx resource add azure-sql`

#### `--function-name`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--function-name`| Да | Укажите имя функции. Значение по умолчанию — `getuserprofile`. |

> [!NOTE]
> Имя функции проверяется как SQL и должно быть доступна из рабочей нагрузки сервера. Если проект не содержит, создайте `Azure Functions`его.

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>Параметры для `teamsfx resource add azure-apim`

> [!TIP]
> Параметры вступает в силу при попытке использовать существующий `APIM` экземпляр. По умолчанию вам не нужно указывать какие-либо параметры, и он создает новый экземпляр на этапе `teamsfx provision` .

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--subscription`| Да | Выбор подписки Azure|
|`--apim-resource-group`| Да| Имя группы ресурсов. |
|`--apim-service-name`| Да | Имя экземпляра службы управления API. |
|`--function-name`| Да | Укажите имя функции. Значение по умолчанию — `getuserprofile`. |

> [!NOTE]
> `Azure API Management` должен работать с `Azure Functions`. Если проект не содержит, `Azure Functions`его можно создать.

## `teamsfx provision`

Подготовьте облачные ресурсы в текущем приложении.

### <a name="parameters-for-teamsfx-provision"></a>Параметры для `teamsfx provision`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да| Выберите среду для проекта. |
|`--subscription`| Нет | Укажите идентификатор подписки Azure. |
|`--resource-group`| Нет | Задайте имя существующей группы ресурсов. |
|`--sql-admin-name`| Нет | Применимо при наличии SQL в проекте. Имя администратора SQL.|
|`--sql-password`| Нет| Применимо при наличии SQL в проекте. Пароль администратора SQL.|

## `teamsfx deploy`

Эта команда используется для развертывания текущего приложения. По умолчанию развертывается весь проект, но его также можно развернуть частично. Несколько параметров: , , , и `teamsbot``spfx`. `apim``function``frontend-hosting`

### <a name="parameters-for-teamsfx-deploy"></a>Параметры для `teamsfx deploy`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да| Выберите существующую среду для проекта. |
|`--open-api-document`| Нет | Применимо, если в проекте есть ресурс APIM. Открытый путь к файлу документа API. |
|`--api-prefix`| Нет | Применимо, если в проекте есть ресурс APIM. Префикс имени API. Уникальное имя API по умолчанию — `{api-prefix}-{resource-suffix}-{api-version}`. |
|`--api-version`| Нет | Применимо, если в проекте есть ресурс APIM. Версия API. |

## `teamsfx validate`

Проверка текущего приложения. Эта команда проверяет файл манифеста приложения.

### <a name="parameters-for-teamsfx-validate"></a>Параметры для `teamsfx validate`

`--env`: выберите существующую среду для проекта.

## `teamsfx publish`

Опубликуйте приложение в Teams.

### <a name="parameters-for-teamsfx-publish"></a>Параметры для `teamsfx publish`

`--env`: выберите существующую среду для проекта.

## `teamsfx package`

Создайте Teams приложения в пакет для публикации.

## `teamsfx preview`

Предварительный просмотр текущего приложения из локального или удаленного приложения.

### <a name="parameters-for-teamsfx-preview"></a>Параметры для `teamsfx preview`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--local`| Нет | Предварительный просмотр приложения из локальной среды. `--local` является монопольным с `--remote`. |
|`--remote`| Нет | Предварительный просмотр приложения из удаленного репозитория. `--remote` является монопольным с `--local`. |
|`--env`| Нет | Выберите существующую среду для проекта при `--remote` добавлении параметра. |
|`--folder`| Нет | Project корневой каталог. Значение по умолчанию — `./`. |
|`--browser`| Нет | Браузер для открытия Teams веб-клиента. Доступны такие параметры `chrome`, как `edge` `default` системный браузер по умолчанию, а значение — . `default`. |
|`--browser-arg`| Нет | Аргумент для передачи в браузер, требуется --browser, может использоваться несколько раз, например --browser-args="--guest" |
|`--sharepoint-site`| Нет | SharePoint URL-адрес сайта, `{your-tenant-name}.sharepoint.com` например для удаленной SPFx проекта. |

### <a name="scenarios-for-teamsfx-preview"></a>Сценарии для `teamsfx preview`

#### <a name="local-preview"></a>Локальная предварительная версия

Зависимости:

* Node.js
* Пакет SDK для .NET
* Функции Azure Core Tools

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>Удаленная предварительная версия

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!NOTE]
> Журналы фоновых служб, например React, сохраняются в `~/.fx/cli-log/local-preview/`.

## `teamsfx config`

Управление данными конфигурации в области действия пользователя или проекта.

| `teamsfx config` Команды  | Описание |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Просмотр значения конфигурации параметра |
| `teamsfx config set <option> <value>` | Обновление значения конфигурации параметра |

### <a name="parameters-for-teamsfx-config"></a>Параметры для `teamsfx config`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Выберите существующую среду для проекта. |
|`--folder`| Нет | Project каталога. Используется для получения или настройки конфигурации проекта. Значение по умолчанию — `./`. |
|`--global`| Нет | Справляться с конфигурацией. Если это так, область ограничена областью пользователя, а не областью проекта. Значение по умолчанию — `false`. В настоящее время поддерживаемые глобальные конфигурации включают `telemetry`, `validate-dotnet-sdk`, `validate-func-core-tools`, . `validate-node` |

### <a name="scenerios-for-teamsfx-config"></a>Scenerios для `teamsfx config`

Секреты в `.userdata` файле шифруются и `teamsfx config` помогают просматривать или обновлять значения.

#### <a name="stop-sending-telemetry-data"></a>Остановка отправки данных телеметрии

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>Отключение средства проверки среды

Существует три конфигурации для включения и отключения Node.js, пакета SDK для .NET и Функции Azure Core Tools, и все они включены по умолчанию. Если вам не нужна проверка зависимостей и вы хотите установить зависимости самостоятельно, можно задать для конфигурации значение off. Ознакомьтесь со следующими руководствами:

* [Node.js установки](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [Руководство по установке пакета SDK для .NET](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
* [Функции Azure по установке Core Tools](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools).

Чтобы отключить проверку пакета SDK для .NET, можно использовать следующую команду:

```bash
teamsfx config set validate-dotnet-sdk off
```

Чтобы включить проверку пакета SDK для .NET, можно использовать следующую команду:

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>Просмотр всех конфигураций области пользователя

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>Просмотр всех конфигураций в проекте

Секрет расшифровывается автоматически:

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>Обновление конфигурации секрета в проекте

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

TeamsFx CLI предоставляет `teamsFx permission` команды для сценария совместной работы.

| `teamsFx permission` Команды | Описание |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | Предоставьте разрешение для учетной записи Microsoft 365 для проекта указанной среды. |
| `teamsfx permission status` | Отображение состояния разрешений для проекта |

### <a name="parameters-for-teamsfx-permission-grant"></a>Параметры для `teamsfx permission grant`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Укажите имя env. |
|`--email`| Да | Укажите адрес электронной почты Microsoft 365 участника совместной работы. Убедитесь, что учетная запись участника совместной работы находится в одном клиенте с создателем. |

### <a name="parameters-for-teamsfx-permission-status"></a>Параметры для `teamsfx permission status`

| Параметр | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Укажите имя env. |
|`--list-all-collaborators` | Нет | С помощью этого флага Teams набор средств CLI выводит всех участников совместной работы для этого проекта. |

### <a name="scenarios-for-teamsfx-permission"></a>Сценарии для `teamsfx permission`

Разрешения для `TeamsFx` проектов перечислены ниже.

#### <a name="grant-permission"></a>Предоставление разрешения

Project автор и участники совместной `teamsfx permission grant` работы могут использовать команду для добавления нового участника совместной работы в проект:

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

Получив необходимое разрешение, создатель проекта и участники совместной работы могут предоставить общий доступ к проекту новому участнику совместной GitHub, а новый участник совместной работы может иметь все разрешения для Microsoft 365 учетной записи.

#### <a name="show-permission-status"></a>Показать состояние разрешения

Project автор и участники `teamsfx permission status` совместной работы могут использовать команду для просмотра Microsoft 365 учетной записи для определенной env:

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>Перечисление всех участников совместной работы

Project автор и участники совместной `teamsfx permission status` работы могут использовать команду для просмотра всех участников совместной работы для конкретной env:

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>Рабочий процесс совместной работы E2E в CLI

Как создатель проекта:

* Чтобы создать вкладку Или проект бота TeamsFx, выберите Azure в качестве типа узла:

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

* Чтобы войти в Microsoft 365 учетной записи Azure, выполните следующее.

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

* Добавление другой учетной записи в качестве участника совместной работы. Убедитесь, что добавленная учетная запись находится в одном клиенте:

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="permission":::

* Отправка проекта в GitHub

Как Project совместной работы:

* Клонируйте проект из GitHub.
* Войдите в Microsoft 365 учетной записи. Убедитесь, что Microsoft 365 добавлена та же учетная запись:

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

* Обновите код вкладки и разверните проект на удаленном компьютере.
* Запустите удаленный компьютер, и проект должен работать нормально.

## <a name="see-also"></a>См. также

* [Пакет SDK TeamsFx для TypeScript или JavaScript](TeamsFx-SDK.md)
* [Управление несколькими средами в наборе средств Teams](TeamsFx-multi-env.md)
* [Совместная работа над Teams проекта с помощью Teams набор средств](TeamsFx-collaboration.md)
* [Обзор набора средств Teams](teams-toolkit-fundamentals.md)
