---
title: Интерфейс командной строки TeamsFx
author: MuyangAmigo
description: Описывает интерфейс командной строки TeamsFx
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 022baf126d8c809bc4f3acb5bcc0496d688a399c
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453665"
---
# <a name="teamsfx-library"></a>Библиотека TeamsFx

Microsoft Teams Framework (TeamsFx) — это библиотека, которая инкапсулирует общие шаблоны функциональности и интеграции (например, упрощенный доступ к Microsoft Identity). Вы можете создавать приложения для Microsoft Teams с нулевой конфигурацией.

Вот список основных функций TeamsFx:

* **TeamsFx Collaboration**: Пусть разработчики и владелец проекта приглашают других сотрудников в проект TeamsFx. Вы можете сотрудничать для отлаговки и развертывания проекта TeamsFx.

* **TeamsFx CLI**: ускоряет разработку Teams приложений. Он также включает сценарий CI/CD, в котором можно интегрировать CLI в скрипты для автоматизации.

* **TeamsFx SDK**: TeamsFx Software Development Kit (SDK) является основной библиотекой кода TeamsFx, инкапсулируя простую проверку подлинности для клиентского и серверного кода, адаптированного для Teams разработчиков.

## <a name="teamsfx-command-line-interface"></a>Интерфейс командной строки TeamsFx

TeamsFx CLI — это интерфейс командной строки на основе текста, который ускоряет Teams разработки приложений. Она направлена на обеспечение работы с клавиатурой при создании Teams приложений. Он также включает сценарий CI/CD, в котором можно интегрировать CLI в скрипты для автоматизации.

Дополнительные сведения см. в статьях:

* [Исходный код](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli)
* [Пакет (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>Начало работы

Установите `teamsfx-cli` и `npm` запустите `teamsfx -h` для проверки всех доступных команд:

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>Поддерживаемые команды

| Команда | Описание |
|----------------|-------------|
| `teamsfx new`| Создание нового Teams приложения.|
| `teamsfx account`| Управление учетной записью облачной службы. Поддерживаемые облачные службы : Azure и Microsoft 365. |
| `teamsfx env` | Управление средами. |
| `teamsfx capability`| Добавьте новые возможности в текущее приложение.|
| `teamsfx resource`  | Управление ресурсами в текущем приложении.|
| `teamsfx provision` | Предоставление облачных ресурсов в текущем приложении.|
| `teamsfx deploy` | Развертывание текущего приложения.  |
| `teamsfx package` | Создайте Teams приложение в пакет для публикации.|
| `teamsfx validate` | Проверка текущего приложения.|
| `teamsfx publish` | Публикация приложения для Teams.|
| `teamsfx preview` | Просмотр текущего приложения. |
| `teamsfx config`  | Управление данными конфигурации. |
| `teamsfx permission`| Сотрудничайте с другими разработчиками в том же проекте.|

## `teamsfx new`

По умолчанию переходит `teamsfx new` в интерактивный режим и направляет вас в процесс создания нового Teams приложения. Вы также можете работать с неинактивным режимом, установив `--interactive` флаг `false`.

| `teamsFx new` Команда | Описание |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Создание приложения из существующего шаблона |
| `teamsfx new template list`     | Список всех доступных шаблонов |

### <a name="parameters-for-teamsfx-new"></a>Параметры для `teamsfx new`

| Параметр | Требования | Описание |
|:---------------- |:-------------|:-------------|
|`--app-name` | Да| Имя вашего Teams приложения.|
|`--interactive`| Нет | Выберите параметры в интерактивном режиме. Параметры и `true` значение `false` по умолчанию `true`.|
|`--capabilities`| Нет| Выберите Teams возможностей приложения, несколько вариантов `tab`, `bot`и `messaging-extension` `tab-spfx`. Значение по умолчанию — `tab`.|
|`--programming-language`| Нет| Язык программирования для проекта. Параметры или значение `javascript` `typescript` по умолчанию `javascript`.|
|`--folder`| Нет | Project каталога. В этом каталоге создается папка sub с именем приложения. Значение по умолчанию — `./`.|
|`--spfx-framework-type`| Нет| Применимо, `Tab(SPfx)` если выбрана возможность. Frontend Framework. Параметры и `none` `react`, и значение по умолчанию `none`.|
|`--spfx-web part-name`| Нет | Применимо, `Tab(SPfx)` если выбрана возможность. Значение по умолчанию — "helloworld".|
|`--spfx-web part-desp`| Нет | Применимо, `Tab(SPfx)` если выбрана возможность. Значение по умолчанию — "helloworld description". |
|`--azure-resources`| Нет| Применимо, если содержит `tab` возможности. Добавьте ресурсы Azure в проект. Это несколько параметров `sql` (База данных SQL Azure) и `function` (Azure Functions). |

### <a name="scenarios-for-teamsfx-new"></a>Сценарии для `teamsfx new`

Вы можете использовать интерактивный режим для создания Teams приложения. Сценарии управления всеми параметрами`teamsfx new`:

#### <a name="tab-app-hosted-on-spfx-using-react"></a>Приложение Tab, которое SPFx с React

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>Teams javaScript с вкладками, возможностями бота и azure Functions

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>Teams вкладка с azure Functions и Azure SQL

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

Управление учетной записью облачной службы. Поддерживаемые облачные службы являются `Azure` и `Microsoft 365`.

| `teamsFx account` Команда | Описание |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | Войдите в выбранную облачную службу. |
| `teamsfx account logout <service>`  | выйти из выбранной облачной службы. |
| `teamsfx account set --subscription` | Обновление параметров учетной записи, чтобы установить ID подписки. |

## `teamsfx env`

Управление средами.

| `teamsfx env` Команда  | Описание |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | Добавьте новую среду путем копирования из указанной среды. |
| `teamsfx env list` | Список всех сред. |

### <a name="scenarios-for-teamsfx-env"></a>Сценарии для `teamsfx env`

Сценарии для `teamsfx env` этого следуют следующим образом:

#### <a name="create-a-new-environment"></a>Создание новой среды

Добавление новой среды путем копирования из существующей среды разработчиков:

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

Добавьте новые возможности в текущее приложение.

| `teamsFx capability` Команда  | Описание |
|:----------------  |:-------------|
| `teamsfx capability add tab` | Добавление вкладки |
| `teamsfx capability add bot` | Добавление бота |
| `teamsfx capability add messaging-extension`| Добавление расширения обмена сообщениями |

> [!NOTE]
> Если в проекте есть бот, расширение обмена сообщениями не может быть добавлено, и оно применяется наоборот. Вы можете включить в проект расширение бота и обмена сообщениями при создании нового Teams приложения.

## `teamsfx resource`

Управление ресурсами в текущем приложении. Поддерживаются `<resource-type>` : `azure-sql`и `azure-function` `azure-apim` .

| `teamsFx resource` Команда  | Описание |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | Добавление ресурса в текущее приложение.|
| `teamsfx resource show <resource-type>`      | Показать сведения о конфигурации ресурса. |
| `teamsfx resource list`      | Список всех ресурсов в текущем приложении. |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>Параметры для `teamsfx resource add azure-function`

| Параметр  | Требования | Описание |
|----------------  |-------------|-------------|
|`--function-name`| Да | Укай имя функции. Значение по умолчанию — `getuserprofile`. |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>Параметры для `teamsfx resource add azure-sql`

#### `--function-name`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--function-name`| Да | Укай имя функции. Значение по умолчанию — `getuserprofile`. |

> [!NOTE]
> Имя функции проверяется как SQL и должно быть доступны из рабочей нагрузки сервера. Если проект не содержит, `Azure Functions`создайте его для вас.

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>Параметры для `teamsfx resource add azure-apim`

> [!TIP]
> Параметры вступает в силу при попытке использования существующего `APIM` экземпляра. По умолчанию не нужно указывать какие-либо параметры, и он создает новый экземпляр во время шага `teamsfx provision` .

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--subscription`| Да | Выберите подписку Azure|
|`--apim-resource-group`| Да| Имя группы ресурсов. |
|`--apim-service-name`| Да | Имя экземпляра службы управления API. |
|`--function-name`| Да | Укай имя функции. Значение по умолчанию — `getuserprofile`. |

> [!NOTE]
> `Azure API Management` необходимо работать с `Azure Functions`. Если проект не содержит, `Azure Functions`можно создать его.

## `teamsfx provision`

Предоставление облачных ресурсов в текущем приложении.

### <a name="parameters-for-teamsfx-provision"></a>Параметры для `teamsfx provision`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да| Выберите среду для проекта. |
|`--subscription`| Нет | Укажите ID подписки Azure. |
|`--resource-group`| Нет | Установите имя существующей группы ресурсов. |
|`--sql-admin-name`| Нет | Применимо при SQL в проекте. Имя администратора SQL.|
|`--sql-password`| Нет| Применимо при SQL в проекте. Пароль администратора SQL.|

## `teamsfx deploy`

Эта команда используется для развертывания текущего приложения. По умолчанию он развертывает весь проект, но также можно развернуть частично. Несколько вариантов , , , и `teamsbot``spfx`. `apim``function``frontend-hosting`

### <a name="parameters-for-teamsfx-deploy"></a>Параметры для `teamsfx deploy`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да| Выберите существующую среду для проекта. |
|`--open-api-document`| Нет | Применимо, если в проекте есть ресурс AIM. Путь к файлу открытого файла API. |
|`--api-prefix`| Нет | Применимо, если в проекте есть ресурс AIM. Префикс имени API. Уникальное имя API `{api-prefix}-{resource-suffix}-{api-version}`по умолчанию . |
|`--api-version`| Нет | Применимо, если в проекте есть ресурс AIM. Версия API. |

## `teamsfx validate`

Проверка текущего приложения. Эта команда проверяет файл манифеста приложения.

### <a name="parameters-for-teamsfx-validate"></a>Параметры для `teamsfx validate`

`--env`: Выберите существующую среду для проекта.

## `teamsfx publish`

Публикация приложения для Teams.

### <a name="parameters-for-teamsfx-publish"></a>Параметры для `teamsfx publish`

`--env`: Выберите существующую среду для проекта.

## `teamsfx package`

Создайте Teams приложение в пакет для публикации.

## `teamsfx preview`

Просмотр текущего приложения из локального или удаленного.

### <a name="parameters-for-teamsfx-preview"></a>Параметры для `teamsfx preview`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--local`| Нет | Просмотр приложения из локального. `--local` является эксклюзивным с `--remote`. |
|`--remote`| Нет | Просмотр приложения с удаленного. `--remote` является эксклюзивным с `--local`. |
|`--env`| Нет | Выберите существующую среду для проекта при `--remote` приложении параметра. |
|`--folder`| Нет | Project корневого каталога. Значение по умолчанию — `./`. |
|`--browser`| Нет | Браузер для открытия Teams веб-клиента. Параметры , такие `chrome``edge` `default` как браузер по умолчанию системы и значение .`default` |
|`--browser-arg`| Нет | Аргумент, который необходимо передать в браузер, требует --browser, можно использовать несколько раз, например--browser-args="--guest" |
|`--sharepoint-site`| Нет | SharePoint url-адрес сайта, `{your-tenant-name}.sharepoint.com` например для SPFx удаленного предварительного просмотра проекта. |

### <a name="scenarios-for-teamsfx-preview"></a>Сценарии для `teamsfx preview`

#### <a name="local-preview"></a>Локальный предварительный просмотр

Зависимости:

* Node.js
* SDK .NET
* Основные средства Azure Functions

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>Удаленный просмотр

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!NOTE]
> Журналы фоновых служб, например React, сохраняются в `~/.fx/cli-log/local-preview/`.

## `teamsfx config`

Управление данными конфигурации в области пользователя или области проекта.

| `teamsfx config` Команда  | Описание |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Просмотр значения конфигурации параметра |
| `teamsfx config set <option> <value>` | Обновление значения параметра конфигурации |

### <a name="parameters-for-teamsfx-config"></a>Параметры для `teamsfx config`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Выберите существующую среду для проекта. |
|`--folder`| Нет | Project каталога. Это используется для получения или настройки конфигурации проекта. Значение по умолчанию — `./`. |
|`--global`| Нет | Справиться с конфигурацией. Если это так, область ограничивается областью пользователей, а не областью проекта. Значение по умолчанию — `false`. В настоящее время поддерживаемые глобальные конфигурации включают `telemetry`, `validate-dotnet-sdk`, `validate-func-core-tools``validate-node`. |

### <a name="scenerios-for-teamsfx-config"></a>Scenerios для `teamsfx config`

Секреты в `.userdata` файле шифруются и `teamsfx config` помогают просматривать или обновлять значения.

#### <a name="stop-sending-telemetry-data"></a>Остановка отправки данных телеметрии

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>Отключение проверки среды

Существует три конфигурации для включения или отключения Node.js, проверки основных средств SDK и Azure Functions, и все они включены по умолчанию. Вы можете настроить конфигурацию на "выключение", если вам не нужна проверка зависимостей и вы хотите самостоятельно установить зависимостей. Ознакомьтесь со следующими руководствами:

* [Node.js установки](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [Руководство по установке SDK .NET](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
* [Руководство по установке основных средств Azure Functions](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools).

Чтобы отключить проверку SDK .NET, можно использовать следующую команду:

```bash
teamsfx config set validate-dotnet-sdk off
```

Чтобы включить проверку SDK .NET, можно использовать следующую команду:

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>Просмотр всей конфигурации области пользователя

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>Просмотр всей конфигурации в проекте

Секрет автоматически расшифровываются:

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>Обновление секретной конфигурации в проекте

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

TeamsFx CLI предоставляет `teamsFx permission` команды для сценария совместной работы.

| `teamsFx permission` команда | Описание |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | Предоставление разрешения для учетной записи Microsoft 365 для проекта указанной среды. |
| `teamsfx permission status` | Показать состояние разрешений для проекта |

### <a name="parameters-for-teamsfx-permission-grant"></a>Параметры для `teamsfx permission grant`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Укай имя env. |
|`--email`| Да | Предопишите адрес электронной почты Microsoft 365 сотрудников. Убедитесь, что учетная запись соавтора находится в одном клиенте с создателем. |

### <a name="parameters-for-teamsfx-permission-status"></a>Параметры для `teamsfx permission status`

| Параметр | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Укай имя env. |
|`--list-all-collaborators` | Нет | С помощью этого флага Teams набор средств CLI печатает всех сотрудников для этого проекта. |

### <a name="scenarios-for-teamsfx-permission"></a>Сценарии для `teamsfx permission`

Разрешения для `TeamsFx` проектов следуют следующим образом:

#### <a name="grant-permission"></a>Разрешение на предоставление

Project разработчики и сотрудники могут использовать команду`teamsfx permission grant`, чтобы добавить в проект нового соавтора:

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

Получив необходимое разрешение, создатель проекта и сотрудники могут поделиться проектом с новым сотрудником GitHub, а новый сотрудник может иметь все разрешения для Microsoft 365 учетной записи.

#### <a name="show-permission-status"></a>Показать состояние разрешений

Project и соавторы `teamsfx permission status` могут использовать команду для просмотра разрешения Microsoft 365 учетной записи для конкретной env:

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>Список всех сотрудников

Project и соавторы могут `teamsfx permission status` использовать команду для просмотра всех сотрудников для конкретного env:

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>Рабочий поток совместной работы E2E в CLI

Как создатель проекта:

* Чтобы создать новый проект вкладки Или бота TeamsFx, выберите Azure в качестве типа хоста:

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

* Чтобы войти в Microsoft 365 учетную запись и учетную запись Azure:

  ```bash
  teamsfx account login azure
  teamsfx account login Microsoft 365
  ```

* Подготовка проекта:

  ```bash
  teamsfx provision
  ```

* Чтобы просмотреть сотрудников:

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-status-all-1.png" alt-text="permission-1":::

* Добавление другой учетной записи в качестве соавтора. Убедитесь, что добавленная учетная запись находится под тем же клиентом:

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="permission":::

* Чтобы подтолкнуть проект к GitHub

В качестве Project сотрудников:

* Клонировать проект из GitHub.
* Вход в Microsoft 365 учетную запись. Убедитесь, что Microsoft 365 будет добавлена та же учетная запись:

  ```bash
  teamsfx account login Microsoft 365
  ```

* Вход в учетную запись Azure с разрешением участника для всех ресурсов Azure.

  ```bash
  teamsfx account login azure
  ```

* Проверка состояния разрешений. У вас должно быть разрешение владельца проекта:

  ```bash
  teamsfx permission status --env dev
  ```

  ![Состояние разрешения](./images/permission-status.png)

* Обнови код вкладки и разверни проект на удаленный.
* Запуск удаленного и проект должен работать нормально.

## <a name="see-also"></a>См. также

* [TeamsFx SDK для TypeScript или JavaScript](TeamsFx-SDK.md)
* [Управление несколькими средами в Teams набор средств](TeamsFx-multi-env.md)
* [Совместное использование Teams с помощью Teams набор средств](TeamsFx-collaboration.md)
